---
icon: elementor
---

# SB-25908: Data migration for all sso users in user\_declaration table

**release-4.2.0**:\
This script will update the school-udise-code and school-name of the sso users in the user-declarations table in up state.

#### Steps to update sso user-declarations: <a href="#sb-25908-datamigrationforallssousersinuser_declarationtable-stepstoupdatessouser-declarations" id="sb-25908-datamigrationforallssousersinuser_declarationtable-stepstoupdatessouser-declarations"></a>

```
vi UserDeclarationIssueupdateUP.scala
copy data from below UserDeclarationIssueupdateUP.scala file  and paste it to  UserDeclarationIssueupdateUP.scala
cd to the spark directory
bin/spark-shell --master local[*] --packages com.datastax.spark:spark-cassandra-connector_2.11:2.5.0
:load {{absolute path of UserDeclarationIssueupdateUP.scala}}
UserDeclarationIssueupdateUP.main("{cassandra ip}")
```

```
import org.apache.spark.sql.functions.{col, _}
import org.apache.spark.sql.{Encoders, SaveMode, SparkSession}
import org.apache.spark.storage.StorageLevel
import java.io.File
import java.io.PrintWriter
import scala.collection.immutable.HashMap


import scala.collection.immutable.HashMap

case class Organisation(id: String, externalid: String, channel: String, istenant: Boolean);

object UserDeclarationIssueupdateUP extends Serializable {

    def main(cassandra: String): Unit = {
        implicit val spark: SparkSession =
            SparkSession
                .builder()
                .appName("UserDeclarationIssueupdateUP")
                .config("spark.master", "local[*]")
                .config("spark.cassandra.connection.host",cassandra)
                .config("spark.cassandra.output.batch.size.rows", "10000")
                .config("spark.cassandra.read.timeoutMS", "60000")
                .getOrCreate()

        val res = time(checkUserDeclarationsUPRecords());

        Console.println("Time taken to execute script", res._1);
        spark.stop();
    }

    def checkUserDeclarationsUPRecords()(implicit spark: SparkSession) {
        import spark.implicits._
        val sparkContext = spark.sparkContext
        val file = new File("userdeclarationup_audit.txt")
        val organisationSchema = Encoders.product[Organisation].schema
        val print_Writer = new PrintWriter(file)
        val orgIdDF = spark.read.format("org.apache.spark.sql.cassandra").schema(organisationSchema).option("keyspace", "sunbird").option("table", "organisation").load().persist(StorageLevel.MEMORY_ONLY)
        val uporgIdDF =   orgIdDF.where(col("channel")==="up" && col("istenant")=== true);
        uporgIdDF.show(10,false)
        val rootOrgIds = uporgIdDF.select(col("id")).as[String].collect()
        val rootOrgId = rootOrgIds(0)
        print_Writer.write("\n up root org id =" + rootOrgId)
        val upSchoolDF = orgIdDF.except(uporgIdDF);
        val userDeclarationsDF = spark.read.format("org.apache.spark.sql.cassandra").option("keyspace", "sunbird").option("table", "user_declarations").load().persist(StorageLevel.MEMORY_ONLY).
            where(col("orgid")=== rootOrgId)
        val userDeclarationsWithSchoolID = userDeclarationsDF.select(col("userid"), col("userid").as("useraliasid"), col("orgid"), col("persona"), col("userinfo").getItem("declared-school-udise-code").as("declared-school-udise-code"),
            col("userinfo").getItem("declared-school-name").as("declared-school-name"), col("userinfo").getItem("declared-email").as("declared-email"),  col("userinfo").getItem("declared-phone").as("declared-phone"),
            col("userinfo").getItem("declared-state").as("declared-state"), col("userinfo").getItem("declared-district").as("declared-district"))
        print_Writer.write("\n userDeclarations with up orgid schhol count =" + userDeclarationsWithSchoolID.count())
        val orgExtIdset = upSchoolDF.select("externalid").collect().map(_(0)).toSeq
        print_Writer.write("\n orgExtIdset =" + orgExtIdset)
        val userDeclarationNESchoolID = userDeclarationsWithSchoolID.where(col("declared-school-udise-code").isNotNull)
        //filtering up user-external id's based on the existing orgext id's
        val newserDeclarationDF = userDeclarationNESchoolID.filter(col("declared-school-udise-code").isin(orgExtIdset:_*));
        val filteredUserDeclarationDF = userDeclarationNESchoolID.except(newserDeclarationDF)
        print_Writer.write("\n user declaration count by removing existing extorg id mapping =" +filteredUserDeclarationDF.count())
        //filteredUserDeclarationDF.show(10,false)
        val oldOrgExtIdDF = spark.read.format("com.databricks.spark.csv").option("header","true")load("/home/analytics/UP_school_org_external_identity_table_deleted_orgs.csv");
        val oldOrgExtIdDFSet = oldOrgExtIdDF.distinct().filter(col("oldexternalid").isNotNull).select("oldexternalid").collect().map(_(0)).toSeq
        print_Writer.write("\n oldOrgExtIdDFLst =" + oldOrgExtIdDFSet)
        //filtering up user-external id's based on the old orgext id's
        val filterOldExtIdDF = filteredUserDeclarationDF.filter(col("declared-school-udise-code").isin(oldOrgExtIdDFSet:_*))
        print_Writer.write("\n user declaration count by removing old extorg id mapping =" +filterOldExtIdDF.count())
        val csvFilteredDF = filterOldExtIdDF.select(col("userid"), col("orgid"), col("persona"), col("declared-school-udise-code"), col("declared-school-name"))
        csvFilteredDF.coalesce(1).write.format("com.databricks.spark.csv").option("header", "true").save("/tmp/userdeclarationinfo")
        val userDecMapInfoDF = filterOldExtIdDF.withColumn("userinfo", userInfoMap(col("declared-email"), col("declared-phone"), col("declared-state"), col("declared-district")))
        val finalUserDeclartion = userDecMapInfoDF.select(col("userid"), col("orgid"), col("persona"), col("userinfo"))
        finalUserDeclartion.write.format("org.apache.spark.sql.cassandra").option("keyspace", "sunbird").option("table", "user_declarations").mode(SaveMode.Append).save();
        print_Writer.close
    }

    def updateUserInfoMapFunction(decEmail: String, decPhone: String, decState: String, decDistrict: String): Map[String, String] = {
        var userInfo = new HashMap[String, String]()
        userInfo += ("declared-school-udise-code" ->  "")
        userInfo += ("declared-school-name" ->  "")
        if(decEmail != null && !decEmail.isEmpty)
            userInfo += ("declared-email" -> decEmail)
        if(decPhone != null && !decPhone.isEmpty)
            userInfo += ("declared-phone" -> decPhone)
        if(decState != null && !decState.isEmpty)
            userInfo += ("declared-state" -> decState)
        if(decDistrict != null && !decDistrict.isEmpty)
            userInfo += ("declared-district" -> decDistrict)
        userInfo
 }

    val userInfoMap = udf[Map[String, String], String, String, String, String](updateUserInfoMapFunction)

    def time[R](block: => R): (Long, R) = {
        val t0 = System.currentTimeMillis()
        val result = block // call-by-name
        val t1 = System.currentTimeMillis()
        ((t1 - t0), result)
    }
}    
```
