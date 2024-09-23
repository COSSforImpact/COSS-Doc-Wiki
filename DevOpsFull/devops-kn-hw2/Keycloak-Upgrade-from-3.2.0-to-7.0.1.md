Steps to upgrade keyclok from version 3.2.0 to 7.0.1


* Create default clients of master realm in the sunbird realm if any of them is deleted


* Go to keycloak admin console and follow the below instructions. Below is an example for one client called admin-cli. If you have more than one default clients deleted, follow same steps for all clients



Go to clients → Create → Provide Client ID  as admin-cli → Disable Standard Flow Enabled → Disable the client by turning off Enabled button → Save


* Login to Jenkins VM and perform the below operations


* Export your postgres connection and database details



export PG_HOST=''  # Enter the postgres host in the quotes

export PG_USER=''  # Enter the postgres user in the quotes

export PG_DB=''       # Enter the keycloak 3 DB name in the quotes

export PGPASSWORD=''   # Enter the postgres password in the quotes


* Create a new directory in jenkins to store all the migration related artefacts



mkdir dev-keycloak7-upgrade

cd dev-keycloak7-upgrade

curl -sS [https://raw.githubusercontent.com/project-sunbird/sunbird-devops/master/deploy/migrate-to-keycloak7.sh](https://raw.githubusercontent.com/project-sunbird/sunbird-devops/master/deploy/migrate-to-keycloak7.sh) --output [migrate-to-keycloak7.sh](http://migrate-to-keycloak7.sh)

chmod 755 migrate-to-keycloak7.sh


* Some important notes before we run the script


    * The script will first take the backup of the current keycloak 3 DB as mentioned by the variable ${PG_DB} above


    * It will create a new database in the name ${PG_DB}7 - Example if your keycloak 3 DB name is keycloak, the script will create a new DB in the name keycloak7


    * The script will restore the keycloak 3 DB to the newly created keyclaok 7 DB


    * The script will also delete duplicate entries in the new DB post restore as these duplicate entries will fail the migration with unique constraint errors. Please see the script to see the delete queries being executed. This wont cause any impact.


    * The script will also truncte all data from the offline tables, since these tables will cause the migration to be slow and it might even fail the start up of keycloak if there are too many rows


    * Removing offline sessions will not logout any mobile app users since that refresh tokens are handled at adminutils layer



    
* The time taken to upgrade will depend on the size of the DB. For a 9GB DB size, the time taken is close to 20-30 minutes. To know the size of the DB, run the below command



SELECT pg_size_pretty( pg_database_size('keycloak') );


* Build keycloak from from [https://github.com/project-sunbird/sunbird-auth/tree/release-3.8.0_RC1](https://github.com/project-sunbird/sunbird-auth/tree/release-3.8.0_RC1)  and ensure ArtifactUplod job is also successful. Your keycloak artifact in jenkins should be showing something in these lines 

keycloak_artifacts.zip:release-3.8.0_RC1_xxxx


* Create a new branch in your private repo for keycloak7. We have created with the name keycloak7


* Update the postgres DB name for keycloak deployment, which should point to the new database ${PG_DB}7



keycloak_postgres_database: ${PG_DB}7  # Replace ${PG_DB} with the actual keycloak 3 DB name


* Remove these variables as they are not required since they have been defined in the all.yml file



keycloak_build_src: "keycloak_build"

keycloak_ver: "keycloak-3.2.0.Final"

keycloak_sms_provider_build: "keycloak-email-phone-autthenticator-1.0-SNAPSHOT.jar"

keycloak_sms_provider_templates_src: "templates.tar.gz"

keycloak_sms_provider_templates_dest: "/opt/keycloak/themes/sunbird/login"

keycloak_ekstep_sunbird_login_theme_file: "login.tar.gz"

keycloak_ekstep_sunbird_login_theme_dest: "/opt/keycloak/themes/sunbird/login"

keycloak_postgresql: "postgresql-9.4.1212.jar"

sunbird_auth_version: 1.0v


* Sample PR for (visible only for those who have access to the private repo) - [https://github.com/ekstep/sunbird-devops/pull/706](https://github.com/ekstep/sunbird-devops/pull/706)


* Stop all the traffic to your environment at the proxy level OR stop the keycloak service so that data does not get updated during the upgrade which might lead to missing users, missing passwords etc.


* Run the migration script and wait for keycloak to start



bash migrate-to-keycloak7.sh


* Once keycloak starts, it will show a message on screen like this, also ensure there are no errors in the keycloak startup



13:36:15,222 INFO  \[org.jboss.as] (Controller Boot Thread) WFLYSRV0060: Http management interface listening on http://127.0.0.1:9990/management

13:36:15,222 INFO  \[org.jboss.as] (Controller Boot Thread) WFLYSRV0051: Admin console listening on http://127.0.0.1:9990

13:36:15,222 INFO  \[org.jboss.as] (Controller Boot Thread) WFLYSRV0025: Keycloak 7.0.1 (WildFly Core 9.0.2.Final) started in 218379ms - Started 682 of 988 services (701 services are lazy, passive or on-demand)


* Verify the admin user is able to login to the admin console using the url [https://JENKINS_IP:8443/auth/](https://27.0.0.11:8443/auth/). Browser will display an insecure message, you can ignore it. Click on the Administration Console and login using the existing admin credentails


* Verify the clients, realms etc are available and same as Keycloak 3 including some of the client credentials. Cassandra federartion page wont open as of now. Once keycloak 7 is deployed, it will open and show the data


* Run keycloak provision



private_branch: keycloak7

branch_or_tag: keycloak7


* Deploy keycloak using the below options



build_number: lastSuccessfulBuild   

 **# Ensure last successful artifact upload job was the keycloak 7 version, if not, give correct build number or use ArtifactRepo as the option to download from blob. In case of dev env, the artifact name is keycloak_artifacts.zip:keycloak7_62a24aa_78** 

private_branch: release-4.4.0

branch_or_tag: release-4.4.0

sunbird_auth_branch_or_tag: release-3.8.0_RC1

# Note, branch is hardcoded in jenkins config since branch_or_tag cannot be overriden as its a global env (valid only for dev and staging env of our Jenkins vm, others can ignore this point)


* Verify Keycloak 7 is up and running and do the checks like login, signup, forgot password etc.


* Set the offline token validity to 3 days on keycloak admin console



Go to keycloak admin console → Login as admin user → Select Sunbird Realm → Click on Tokens Tab → Change value of Offline Session Idle as 3 days


* Update brute force configration



Go to http://keycloak_ip/auth/admin/master/console/#/realms/sunbird/defense/brute-force → Set the values shows as per the below image

![](images/storage/Screenshot%20from%202021-03-17%2014-27-46.png)
* Go to http://{{KEYCLOAK_IP}}/auth/admin/master/console/#/realms/sunbird/keys. You will have 3 keys as shown in the below picture



![](images/storage/Screenshot%20from%202021-03-30%2011-38-05.png)
* Click on  **hmac-generated** and set the values as shown in the below image



![](images/storage/Screenshot%20from%202021-03-30%2011-39-23.png)
* Get this secret key value from the postgres keycloak 7 DB by running the below query




```
SELECT value FROM component_config CC INNER JOIN component C ON(CC.component_id = C.id) WHERE C.realm_id = 'sunbird' and provider_id = 'hmac-generated' AND CC.name = 'secret';
```

* Add a new variable in Core/secrets.yml as show below




```
adminutil_refresh_token_secret_key: "VALUE FROM THE ABOVE QUERY"
```

* Build Adminutils from release-3.7.0_RC1 and deploy Adminutils from release-3.7.0_RC15





 **Note:** 


* For environments where keycloak was upgraded to version 6 and rolled back, they need to do the following additional manual steps in case of failed migrations. This is on a case to case basis.


* If the above keycloak migration fails with exceptions, please take a look at the exception and work towards a solution for fixing the exceptions. Most of the time the exceptions are  self sufficient to understand as to why it failed and what you should do to fix it


* Some steps which were run on dev env



psql -h $PG_HOST -U $PG_USER -d ${PG_DB}7

drop table databasechangelog;

ALTER TABLE public.USER_ENTITY DROP COLUMN NOT_BEFORE;

\q

curl -sS [https://raw.githubusercontent.com/project-sunbird/sunbird-devops/keycloak7/ansible/roles/keycloak-deploy/templates/databasechangelog.sql](https://raw.githubusercontent.com/project-sunbird/sunbird-devops/keycloak7/ansible/roles/keycloak-deploy/templates/databasechangelog.sql) --output [databasechangelog.sql](https://github.com/project-sunbird/sunbird-devops/blob/keycloak7/ansible/roles/keycloak-deploy/templates/databasechangelog.sql)

psql -h $PG_HOST -U $PG_USER -d ${PG_DB}7 < databasechangelog.sql

ip="$(ifconfig | grep -A 1 'eth0' | tail -1 | cut -d ':' -f 2 | cut -d ' ' -f 1)"

cd keycloak-7.0.1

bin/standalone.sh -b=$ip -bprivate=$ip --server-config standalone-ha.xml



 **Rollback keycloak from version 7 to version 3** 


* Rollback is very simple


* Either build keycloak from release-3.6.0_RC1 tag or use an already existing artifact of this version (in jenkins job or artifact repo). Artifact name is [keycloak_artifacts.zip:release-3.6.0_RC1](https://10.20.0.14/jenkins/job/Deploy/job/staging/job/Kubernetes/job/Keycloak/lastSuccessfulBuild/artifact/keycloak_artifacts.zip%3Arelease-3.6.0_RC1)


* Use the release-3.8.0 branch to redeploy keycloak



build_number: CHOOSE APPROPRIATELY FROM JENKINS

OR use option ArtifactRepo for artifact_source and use below version

artifact_version: [keycloak_artifacts.zip:release-3.6.0_RC1](https://10.20.0.14/jenkins/job/Deploy/job/staging/job/Kubernetes/job/Keycloak/lastSuccessfulBuild/artifact/keycloak_artifacts.zip%3Arelease-3.6.0_RC1)

private_branch: release-3.8.0

branch_or_tag: release-3.8.0

sunbird_auth_branch_or_tag: release-3.6.0_RC1

# Note, branch is hardcoded in jenkins config since branch_or_tag cannot be overriden as its a global env, so modify accordingly before deploy (valid only for dev and staging env of our Jenkins vm, others can ignore this point)


* Undoing the changes of the provision job for keycloak 7 is not required for rollback since it  will work fine even with keycloak 3





*****

[[category.storage-team]] 
[[category.confluence]] 
