---
icon: folder-open
---

# Optimize docker image for Sunbird LMS service

## **Overview** <a href="#optimizedockerimageforsunbirdlmsservice-overview" id="optimizedockerimageforsunbirdlmsservice-overview"></a>

The current size of docker image of **sunbird-lms service** is approximately **1.16-1.17GB,** But the compressed JAR of **learnin-service** having max size **250MB** approx .  We have to find the approach to optimize the docker image .This can be done by removing unwanted files and **maven dependencies**  from **learning-service** repository and **pom.xml** respectively, but it will not have a big impact as of now files included into jar which are not java files weight below 1 MB and maven dependencies are added after only code review. So Better approach will be to explore **docker image and its build process**.\
\
\


**Approach 1:**

Changing version of the dependency used in project to a same version number and removing unwanted or already add dependencies which are being inherited from another module.\
After Implementing this approach no significant difference in the JAR size, but it is good practice to use same version of a dependency all over the project.

\


**Approach 2:**

This approach is to explore and understand how docker images are created and how we are creating the docker image of **LMS** .

The build steps and output used to create docker image on server are below :

\
we use the script "Build.sh" for creating the docker image, content of script are as follows:

**Build.sh**

```
#!/bin/sh
# Build script
# set -o errexit
e () {
    echo $( echo ${1} | jq ".${2}" | sed 's/\"//g')
}
m=$(./metadata.sh)

org=$(e "${m}" "org")
name=$(e "${m}" "name")
version=$(e "${m}" "version")
# docker build -f "./learner-actors/actors/Dockerfile.test" -t sunbird/actor-service:0.0.1-build .
# docker run --name actor-service-0.0.1-build sunbird/actor-service:0.0.1-build
# containerid=`docker ps -q -a -f name=actor-service-0.0.1-build`
# docker cp $containerid:/opt/learner-actors/actors/learner-actor/target/learner-actor-1.0-SNAPSHOT.jar ./learner-actors/actors/learner-actor-1.0-SNAPSHOT.jar
#docker rm $containerid
docker build -f ./Dockerfile -t ${org}/${name}:${version}-bronze .
```

\


The content of **Dockerfile** which is used in Build.sh

```
FROM openjdk:8-jdk-alpine
MAINTAINER "Manojv" "manojv@ilimi.in"
RUN apk update \
    && apk add unzip \
    && apk add curl \
    && adduser -u 1001 -h /home/sunbird/ -D sunbird \
    && mkdir -p /home/sunbird/learner
COPY ./service/target/actor-service.jar /home/sunbird/learner/
RUN chown -R sunbird:sunbird /home/sunbird
EXPOSE 8088
USER sunbird
WORKDIR /home/sunbird/learner/
CMD ["java", "-cp", "actor-service.jar", "-Dactor_hostname=actor-service", "-Dbind_hostname=0.0.0.0", "org.sunbird.middleware.Application"]
```

After running the following command:

```
sudo docker build -f Dockerfile -t org/sunb:mayank-bronze1 .
```

output were as follows :

```
Sending build context to Docker daemon  331.9MB
Step 1/9 : FROM openjdk:8-jre-alpine
 ---> 556cf01c8299
Step 2/9 : MAINTAINER "Manojv" "manojv@ilimi.in"
 ---> Using cache
 ---> 4d6b65b40c4b
Step 3/9 : RUN apk update     && apk add  unzip     && apk add curl     && adduser -u 1001 -h /home/sunbird/ -D sunbird     && mkdir -p /home/sunbird/learner
 ---> Using cache
 ---> 6eb982c6b85a
Step 4/9 : COPY ./service/target/learning-service-1.0-SNAPSHOT-dist.zip /home/sunbird/learner/
 ---> 6a60144252a8
Step 5/9 : RUN unzip /home/sunbird/learner/learning-service-1.0-SNAPSHOT-dist.zip -d /home/sunbird/learner/
 ---> Running in 929164e0e671
Archive:  /home/sunbird/learner/learning-service-1.0-SNAPSHOT-dist.zip
   creating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/
   creating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/learning-service-1.0-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-compute-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.jcip.jcip-annotations-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.sun.mail.javax.mail-1.6.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.microsoft.azure.azure-storage-5.4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.digitalocean2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.slf4j-log4j12-1.7.10.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.htrace.htrace-core-3.1.0-incubating.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.protobuf.protobuf-java-2.5.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.elasticsearch-util-1.0-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-jaxrs-services-3.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.sun.jersey.jersey-json-1.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.slf4j-api-1.7.12.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.inject.guice-4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.velocity.velocity-tools-2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.struts.struts-tiles-1.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/joda-time.joda-time-2.8.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.profitbricks-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-spatial3d-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-sqs-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.skalicloud-sdg-my-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudservers-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-3.10.4.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/sslext.sslext-1.2-0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.cloudstack-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/ch.qos.logback.logback-classic-1.1.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.ssl-config-core_2.11-0.2.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-okhttp-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-protobuf_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.elastichosts-lon-p-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jzlib-1.1.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-actor_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.config-1.3.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-trove-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.modules.scala-xml_2.11-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.packet-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-sshj-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-auth-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/dom4j.dom4j-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.sqs-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-cloudloadbalancers-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-functional_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.jaxrs.jackson-jaxrs-base-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.modules.scala-java8-compat_2.11-0.7.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-suggest-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.lmax.disruptor-3.2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-net.commons-net-3.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-memory-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.netty.netty-http-pipelining-1.1.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/ch.qos.logback.logback-core-1.1.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.byon-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-azure-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddatabases-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.docker-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-jaxrs-1.8.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.jul-to-slf4j-1.7.12.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/antlr.antlr-2.7.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.elasticstack-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-cloudidentity-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.tukaani.xz-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-transport-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.mashape.unirest.unirest-java-1.4.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-exceptions-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.datatype.jackson-datatype-jdk8-2.5.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.inject.extensions.guice-multibindings-3.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.module.jackson-module-paranamer-2.7.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.logging.log4j.log4j-api-2.8.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.keycloak.keycloak-common-3.2.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.hk2.osgi-resource-locator-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.reindex-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpasyncclient-4.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-queryparser-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudblockstorage-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.client.rest-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-stream_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.google-cloud-storage-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.mortbay.jetty.jetty-6.1.26.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-buffer-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-all-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.servlet.servlet-api-2.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.java.dev.jets3t.jets3t-0.9.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.mail.javax.mail-api-1.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.xerial.snappy.snappy-java-1.0.4.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-remote_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.spec.javax.ws.rs.jboss-jaxrs-api_2.0_spec-1.0.1.Beta1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.transport-netty3-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.core.jackson-databind-2.9.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.atmos-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-join-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.datatype.jackson-datatype-jsr310-2.5.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-route53-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.java.dev.jna.jna-platform-4.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.keycloak.keycloak-admin-client-3.2.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/log4j.log4j-1.2.17.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.scala-library-2.11.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpmime-4.5.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.curator.curator-framework-2.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.curator.curator-recipes-2.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-netty-utils-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.struts.struts-taglib-1.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-codec-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.server.apacheds-kerberos-codec-2.0.0-M15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.sun.xml.bind.jaxb-impl-2.2.3-1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.jcl-over-slf4j-1.7.12.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-math3-3.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.yaml.snakeyaml-1.17.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.hierynomus.sshj-0.20.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.chef-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.dataformat.jackson-dataformat-cbor-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-misc-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.core.jackson-annotations-2.9.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-mapper-asl-1.9.13.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddns-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.servlet.jsp.jsp-api-2.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.reactivestreams.reactive-streams-1.0.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.b2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.ec2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.agrona.agrona-0.9.18.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-stm.scala-stm_2.11-0.7.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-allblobstore-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.dynect-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.squareup.okio.okio-1.2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.logging.log4j.log4j-core-2.8.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.softlayer-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-spatial-extras-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-resolver-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.moparisthebest.junidecode-0.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-configuration.commons-configuration-1.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-digester.commons-digester-1.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudfiles-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.server.apacheds-i18n-2.0.0-M15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-jackson2-provider-3.1.3.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-highlighter-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.build-link-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-allcompute-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-ec2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.elastichosts-lon-b-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.curator.curator-client-2.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.azurecompute-arm-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpcore-4.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-cli.commons-cli-1.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-netty-server_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.bouncycastle.bcprov-jdk15on-1.52.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.bouncycastle.bcprov-ext-jdk15on-1.51.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-csv-1.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.sf.jopt-simple.jopt-simple-5.0.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.xmlbeans.xmlbeans-2.6.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.go2cloud-jhb1-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-loadbalancer-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.java.dev.jna.jna-3.4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.sshj-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-annotations-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.core-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-clouddns-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.aeron.aeron-client-1.9.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-sts-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.usocket-jna-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-analyzers-common-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.azureblob-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.scala-reflect-2.11.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jamesmurty.utils.java-xmlbuilder-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.sshagent-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-httpclient.commons-httpclient-3.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-lang3-3.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-s3-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.core.jackson-core-2.9.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.velocity.velocity-1.6.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-slf4j_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-handler-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.elastichosts-sat-p-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/aopalliance.aopalliance-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.lang-mustache-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.thoughtworks.paranamer.paranamer-2.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.i2p.crypto.eddsa-0.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudservers-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.sts-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/xml-apis.xml-apis-1.4.01.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.cloudwatch-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-allloadbalancer-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.module.jackson-module-scala_2.11-2.7.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-jaxrs-3.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.squareup.okhttp.okhttp-2.2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-common-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.googlecode.libphonenumber.libphonenumber-8.10.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.annotation.jsr250-api-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.usocket-nc-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.errorprone.error_prone_annotations-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-logging.commons-logging-1.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-core-asl-1.9.13.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.carrotsearch.hppc-0.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.module.jackson-module-jaxb-annotations-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.validation.validation-api-1.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudfiles-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.jaxrs-api-3.0.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-sandbox-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.route53-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-collections.commons-collections-3.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.tika.tika-core-1.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-swift-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.xml.bind.jaxb-api-2.2.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.github.spullara.mustache.java.compiler-0.9.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.hdrhistogram.HdrHistogram-2.1.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.struts.struts-core-1.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.serverlove-z1-man-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.activation.activation-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.jaxrs.jackson-jaxrs-json-provider-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.code.findbugs.jsr305-2.0.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-chain.commons-chain-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.zookeeper.zookeeper-3.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-collections4-4.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/xerces.xercesImpl-2.11.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.actor-util-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.hk2.external.javax.inject-2.5.0-b42.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.percolator-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-codec.commons-codec-1.10.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.request-validator-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.joda.joda-convert-1.7.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudloadbalancers-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.core.jersey-client-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.inject.javax.inject-1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.filesystem-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-beanutils.commons-beanutils-core-1.8.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.transaction.jta-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.xml.stream.stax-api-1.0-2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.guava.guava-18.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.dataformat.jackson-dataformat-yaml-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.core.jersey-server-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch-0.1.42.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-spatial-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddatabases-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.elasticsearch-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/oro.oro-2.0.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.logging.jboss-logging-3.3.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/stax.stax-api-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudblockstorage-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.javassist.javassist-3.19.0-GA.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.dataformat.jackson-dataformat-smile-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddns-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.tdunning.t-digest-3.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.ultradns-ws-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.gogrid-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-xc-1.8.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.transport-netty4-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.common.googlecloud-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.ws.rs.javax.ws.rs-api-2.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-lang.commons-lang-2.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-core-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.google-compute-engine-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-compress-1.4.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-iteratees_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.pageant-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-nova-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-backward-codecs-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudloadbalancers-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.poi.poi-ooxml-schemas-3.15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.github.virtuald.curvesapi-1.04.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.mw-service-1.0-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.mortbay.jetty.jetty-util-6.1.26.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-client-3.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-bouncycastle-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.modules.scala-parser-combinators_2.11-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-server_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.microsoft.azure.azure-keyvault-core-0.8.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/xmlenc.xmlenc-0.52.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpcore-nio-4.4.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.client.transport-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.jna-4.4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.api.api-util-1.0.0-M20.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.connector-factory-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-core-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpclient-4.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.spec.javax.annotation.jboss-annotations-api_1.2_spec-1.0.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.inject.extensions.guice-assistedinject-4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-neutron-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.api.api-asn1-api-1.0.0-M20.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.keycloak.keycloak-core-3.2.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-slf4j-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-io.commons-io-2.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-common-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-grouping-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-beanutils.commons-beanutils-1.7.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-scriptbuilder-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.poi.poi-ooxml-3.15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.twirl-api_2.11-1.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-cloudwatch-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-datacommons_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.oauth-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.bouncycastle.bcpkix-jdk15on-1.52.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.common-util-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.code.gson.gson-2.8.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.s3-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.models-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.iharder.base64-2.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.annotation.javax.annotation-api-1.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.openhosting-east1-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.media.jersey-media-jaxb-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-cinder-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.securesm-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-queries-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-blobstore-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-nova-ec2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jettison.jettison-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-codec-http-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-json_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-cloudfiles-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.core.jersey-common-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.aeron.aeron-driver-1.9.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-validator.commons-validator-1.3.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-keystone-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.json.json-20090211.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.poi.poi-3.15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.avro.avro-1.7.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.cloud-store-sdk-1.2.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/start  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/start.bat  
Removing intermediate container 929164e0e671
 ---> ad02094fda84
Step 6/9 : RUN chown -R sunbird:sunbird /home/sunbird
 ---> Running in 8c8c9a31211d
Removing intermediate container 8c8c9a31211d
 ---> c2ea613e9cc6
Step 7/9 : USER sunbird
 ---> Running in ba0347ab256b
Removing intermediate container ba0347ab256b
 ---> 571efad09e1c
Step 8/9 : WORKDIR /home/sunbird/learner/
 ---> Running in a95a9eae71ae
Removing intermediate container a95a9eae71ae
 ---> 956840558ab4
Step 9/9 : CMD java  -cp '/home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/*' play.core.server.ProdServerStart  /home/sunbird/learner/learning-service-1.0-SNAPSHOT
 ---> Running in 803d3abc6f68
Removing intermediate container 803d3abc6f68
 ---> 3a3c00ffda48
Successfully built 3a3c00ffda48
Successfully tagged org/sunb:mayank-bronze1
```

\


Use following command to obtain details about image created in above step.

```
sudo docker images
```

Output:

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
org/sunb            mayank-bronze1      3a3c00ffda48        8 seconds ago       1.17GB
openjdk             8-jre-alpine        556cf01c8299        4 hours ago         83.1MB
```

\


So the the docker image we have created have size **1.17GB**, but  if we take a look on the size of **learning-service-1.0-SNAPSHOT-dist.zip** is **244MB** approx.\
If we assume the compression ratio to be 0.5 (very idea case), the max size should be **500MB.** So total size of docker image should not exceed 600-800MB approximetaly.

### **How above process works ?** <a href="#optimizedockerimageforsunbirdlmsservice-howaboveprocessworks" id="optimizedockerimageforsunbirdlmsservice-howaboveprocessworks"></a>

Every command in a Dockerfile runs in a separate (intermediate) container. The results are then stored as a new image layer on top of the existing ones. Adding a file in one layer and then removing, replacing or even moving it in another layer does not remove the original file from the underlying layer. Think of layers as of Git commits — a file is preserved in the git history even after you remove it from the repo.

Updating ownership on a file with **chown** effectively results in duplicating that file and storing its new copy in a new layer. The original copy is still there in the underlying layer. The same applies to **chmod** and even **mv** commands. When using them in your Dokerfile, you may end up with an inflated image, before you realize what’s going on.

As a workaround and the best practice multiple **RUN** commands in a Dockerfile should be logically grouped together, making sure that any download, move/remove, permission setting operations happen in the same intermediate container and thus committed in the same image layer.

Changes Suggested in the Dockerfile : changing the execution order of the script so we can reduce the size of image by use above concept.

```
FROM openjdk:8-jre-alpine
MAINTAINER "Manojv" "manojv@ilimi.in"
RUN apk update \
    && apk add  unzip \
    && apk add curl \
    && adduser -u 1001 -h /home/sunbird/ -D sunbird \
    && mkdir -p /home/sunbird/learner
#ENV sunbird_learnerstate_actor_host 52.172.24.203
#ENV sunbird_learnerstate_actor_port 8088 
RUN chown -R sunbird:sunbird /home/sunbird
COPY ./service/target/learning-service-1.0-SNAPSHOT-dist.zip /home/sunbird/learner/
RUN unzip /home/sunbird/learner/learning-service-1.0-SNAPSHOT-dist.zip -d /home/sunbird/learner/
USER sunbird
WORKDIR /home/sunbird/learner/
CMD java  -cp '/home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/*' play.core.server.ProdServerStart  /home/sunbird/learner/learning-service-1.0-SNAPSHOT
```

After running the above script :

```
Sending build context to Docker daemon  331.9MB
Step 1/9 : FROM openjdk:8-jre-alpine
 ---> 556cf01c8299
Step 2/9 : MAINTAINER "Manojv" "manojv@ilimi.in"
 ---> Using cache
 ---> 4d6b65b40c4b
Step 3/9 : RUN apk update     && apk add  unzip     && apk add curl     && adduser -u 1001 -h /home/sunbird/ -D sunbird     && mkdir -p /home/sunbird/learner
 ---> Using cache
 ---> 6eb982c6b85a
Step 4/9 : RUN chown -R sunbird:sunbird /home/sunbird
 ---> Running in 62996bad39cf
Removing intermediate container 62996bad39cf
 ---> 93c324251e6c
Step 5/9 : COPY ./service/target/learning-service-1.0-SNAPSHOT-dist.zip /home/sunbird/learner/
 ---> 0dbd1bbcaf3d
Step 6/9 : RUN unzip /home/sunbird/learner/learning-service-1.0-SNAPSHOT-dist.zip -d /home/sunbird/learner/
 ---> Running in 560deefaeb0d
Archive:  /home/sunbird/learner/learning-service-1.0-SNAPSHOT-dist.zip
   creating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/
   creating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/learning-service-1.0-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-compute-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.jcip.jcip-annotations-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.sun.mail.javax.mail-1.6.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.microsoft.azure.azure-storage-5.4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.digitalocean2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.slf4j-log4j12-1.7.10.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.htrace.htrace-core-3.1.0-incubating.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.protobuf.protobuf-java-2.5.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.elasticsearch-util-1.0-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-jaxrs-services-3.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.sun.jersey.jersey-json-1.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.slf4j-api-1.7.12.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.inject.guice-4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.velocity.velocity-tools-2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.struts.struts-tiles-1.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/joda-time.joda-time-2.8.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.profitbricks-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-spatial3d-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-sqs-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.skalicloud-sdg-my-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudservers-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-3.10.4.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/sslext.sslext-1.2-0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.cloudstack-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/ch.qos.logback.logback-classic-1.1.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.ssl-config-core_2.11-0.2.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-okhttp-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-protobuf_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.elastichosts-lon-p-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jzlib-1.1.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-actor_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.config-1.3.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-trove-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.modules.scala-xml_2.11-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.packet-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-sshj-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-auth-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/dom4j.dom4j-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.sqs-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-cloudloadbalancers-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-functional_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.jaxrs.jackson-jaxrs-base-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.modules.scala-java8-compat_2.11-0.7.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-suggest-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.lmax.disruptor-3.2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-net.commons-net-3.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-memory-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.netty.netty-http-pipelining-1.1.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/ch.qos.logback.logback-core-1.1.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.byon-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-azure-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddatabases-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.docker-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-jaxrs-1.8.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.jul-to-slf4j-1.7.12.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/antlr.antlr-2.7.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.elasticstack-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-cloudidentity-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.tukaani.xz-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-transport-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.mashape.unirest.unirest-java-1.4.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-exceptions-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.datatype.jackson-datatype-jdk8-2.5.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.inject.extensions.guice-multibindings-3.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.module.jackson-module-paranamer-2.7.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.logging.log4j.log4j-api-2.8.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.keycloak.keycloak-common-3.2.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.hk2.osgi-resource-locator-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.reindex-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpasyncclient-4.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-queryparser-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudblockstorage-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.client.rest-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-stream_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.google-cloud-storage-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.mortbay.jetty.jetty-6.1.26.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-buffer-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-all-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.servlet.servlet-api-2.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.java.dev.jets3t.jets3t-0.9.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.mail.javax.mail-api-1.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.xerial.snappy.snappy-java-1.0.4.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-remote_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.spec.javax.ws.rs.jboss-jaxrs-api_2.0_spec-1.0.1.Beta1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.transport-netty3-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.core.jackson-databind-2.9.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.atmos-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-join-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.datatype.jackson-datatype-jsr310-2.5.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-route53-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.java.dev.jna.jna-platform-4.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.keycloak.keycloak-admin-client-3.2.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/log4j.log4j-1.2.17.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.scala-library-2.11.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpmime-4.5.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.curator.curator-framework-2.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.curator.curator-recipes-2.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-netty-utils-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.struts.struts-taglib-1.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-codec-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.server.apacheds-kerberos-codec-2.0.0-M15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.sun.xml.bind.jaxb-impl-2.2.3-1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.slf4j.jcl-over-slf4j-1.7.12.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-math3-3.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.yaml.snakeyaml-1.17.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.hierynomus.sshj-0.20.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.chef-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.dataformat.jackson-dataformat-cbor-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-misc-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.core.jackson-annotations-2.9.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-mapper-asl-1.9.13.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddns-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.servlet.jsp.jsp-api-2.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.reactivestreams.reactive-streams-1.0.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.b2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.ec2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.agrona.agrona-0.9.18.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-stm.scala-stm_2.11-0.7.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-allblobstore-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.dynect-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.squareup.okio.okio-1.2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.logging.log4j.log4j-core-2.8.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.softlayer-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-spatial-extras-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-resolver-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.moparisthebest.junidecode-0.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-configuration.commons-configuration-1.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-digester.commons-digester-1.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudfiles-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.server.apacheds-i18n-2.0.0-M15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-jackson2-provider-3.1.3.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-highlighter-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.build-link-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-allcompute-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-ec2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.elastichosts-lon-b-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.curator.curator-client-2.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.azurecompute-arm-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpcore-4.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-cli.commons-cli-1.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-netty-server_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.bouncycastle.bcprov-jdk15on-1.52.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.bouncycastle.bcprov-ext-jdk15on-1.51.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-csv-1.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.sf.jopt-simple.jopt-simple-5.0.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.xmlbeans.xmlbeans-2.6.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.go2cloud-jhb1-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-loadbalancer-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.java.dev.jna.jna-3.4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.sshj-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-annotations-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.core-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-clouddns-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.aeron.aeron-client-1.9.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-sts-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.usocket-jna-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-analyzers-common-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.azureblob-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.scala-reflect-2.11.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jamesmurty.utils.java-xmlbuilder-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.sshagent-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-httpclient.commons-httpclient-3.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-lang3-3.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-s3-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.core.jackson-core-2.9.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.velocity.velocity-1.6.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.akka.akka-slf4j_2.11-2.5.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-handler-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.elastichosts-sat-p-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/aopalliance.aopalliance-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.lang-mustache-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.thoughtworks.paranamer.paranamer-2.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.i2p.crypto.eddsa-0.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudservers-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.sts-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/xml-apis.xml-apis-1.4.01.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.cloudwatch-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-allloadbalancer-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.module.jackson-module-scala_2.11-2.7.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-jaxrs-3.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.squareup.okhttp.okhttp-2.2.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-common-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.googlecode.libphonenumber.libphonenumber-8.10.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.annotation.jsr250-api-1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.usocket-nc-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.errorprone.error_prone_annotations-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-logging.commons-logging-1.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-core-asl-1.9.13.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.carrotsearch.hppc-0.7.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.module.jackson-module-jaxb-annotations-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.validation.validation-api-1.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudfiles-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.jaxrs-api-3.0.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-sandbox-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.route53-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-collections.commons-collections-3.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.tika.tika-core-1.16.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-swift-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.xml.bind.jaxb-api-2.2.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.github.spullara.mustache.java.compiler-0.9.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.hdrhistogram.HdrHistogram-2.1.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.struts.struts-core-1.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.serverlove-z1-man-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.activation.activation-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.jaxrs.jackson-jaxrs-json-provider-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.code.findbugs.jsr305-2.0.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-chain.commons-chain-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.zookeeper.zookeeper-3.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-collections4-4.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/xerces.xercesImpl-2.11.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.actor-util-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.hk2.external.javax.inject-2.5.0-b42.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.percolator-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-codec.commons-codec-1.10.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.request-validator-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.joda.joda-convert-1.7.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudloadbalancers-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.core.jersey-client-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.inject.javax.inject-1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.filesystem-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-beanutils.commons-beanutils-core-1.8.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.transaction.jta-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.xml.stream.stax-api-1.0-2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.guava.guava-18.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.dataformat.jackson-dataformat-yaml-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.core.jersey-server-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch-0.1.42.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-spatial-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddatabases-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.elasticsearch-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/oro.oro-2.0.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.logging.jboss-logging-3.3.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/stax.stax-api-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudblockstorage-us-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.javassist.javassist-3.19.0-GA.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.fasterxml.jackson.dataformat.jackson-dataformat-smile-2.8.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-clouddns-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.tdunning.t-digest-3.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.ultradns-ws-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.gogrid-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jackson.jackson-xc-1.8.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.plugin.transport-netty4-client-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.common.googlecloud-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.ws.rs.javax.ws.rs-api-2.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-lang.commons-lang-2.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-core-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.google-compute-engine-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.commons.commons-compress-1.4.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-iteratees_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.pageant-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-nova-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-backward-codecs-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.rackspace-cloudloadbalancers-uk-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.poi.poi-ooxml-schemas-3.15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.github.virtuald.curvesapi-1.04.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.mw-service-1.0-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.mortbay.jetty.jetty-util-6.1.26.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.resteasy.resteasy-client-3.1.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-bouncycastle-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.scala-lang.modules.scala-parser-combinators_2.11-1.0.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-server_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.microsoft.azure.azure-keyvault-core-0.8.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/xmlenc.xmlenc-0.52.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpcore-nio-4.4.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.client.transport-5.4.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.jna-4.4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.api.api-util-1.0.0-M20.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.jcraft.jsch.agentproxy.connector-factory-0.0.9.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-core-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.httpcomponents.httpclient-4.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.jboss.spec.javax.annotation.jboss-annotations-api_1.2_spec-1.0.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.inject.extensions.guice-assistedinject-4.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-neutron-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.directory.api.api-asn1-api-1.0.0-M20.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.keycloak.keycloak-core-3.2.0.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.driver.jclouds-slf4j-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-io.commons-io-2.5.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.hadoop.hadoop-common-2.7.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-grouping-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-beanutils.commons-beanutils-1.7.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-scriptbuilder-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.poi.poi-ooxml-3.15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.twirl-api_2.11-1.1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.aws-cloudwatch-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-datacommons_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.oauth-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.bouncycastle.bcpkix-jdk15on-1.52.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.common-util-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.google.code.gson.gson-2.8.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.s3-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.models-0.0.1-SNAPSHOT.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/net.iharder.base64-2.3.8.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/javax.annotation.javax.annotation-api-1.2.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.provider.openhosting-east1-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.media.jersey-media-jaxb-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-cinder-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.elasticsearch.securesm-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.lucene.lucene-queries-6.5.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.jclouds-blobstore-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-nova-ec2-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.codehaus.jettison.jettison-1.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.netty.netty-codec-http-4.1.11.Final.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/com.typesafe.play.play-json_2.11-2.4.6.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.rackspace-cloudfiles-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.glassfish.jersey.core.jersey-common-2.27.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/io.aeron.aeron-driver-1.9.3.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/commons-validator.commons-validator-1.3.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.jclouds.api.openstack-keystone-2.1.0.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.json.json-20090211.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.poi.poi-3.15.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.apache.avro.avro-1.7.4.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/org.sunbird.cloud-store-sdk-1.2.1.jar  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/start  
  inflating: /home/sunbird/learner/learning-service-1.0-SNAPSHOT/start.bat  
Removing intermediate container 560deefaeb0d
 ---> 4db6112ad209
Step 7/9 : USER sunbird
 ---> Running in e20ac252b596
Removing intermediate container e20ac252b596
 ---> c2cb63c11755
Step 8/9 : WORKDIR /home/sunbird/learner/
 ---> Running in a35f9aeb5019
Removing intermediate container a35f9aeb5019
 ---> ce50b5801afe
Step 9/9 : CMD java  -cp '/home/sunbird/learner/learning-service-1.0-SNAPSHOT/lib/*' play.core.server.ProdServerStart  /home/sunbird/learner/learning-service-1.0-SNAPSHOT
 ---> Running in 632a07bfb85b
Removing intermediate container 632a07bfb85b
 ---> 6a2c3633fa4d
Successfully built 6a2c3633fa4d
Successfully tagged org1/sunb2:mayank-bronze6

```

Use following command to obtain details about image created in above step.

```
sudo docker images
```

Output :

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
org1/sunb2          mayank-bronze6      6a2c3633fa4d        8 seconds ago       630MB
org/sunb            mayank-bronze1      3a3c00ffda48        About an hour ago   1.17GB
openjdk             8-jre-alpine        556cf01c8299        5 hours ago         83.1MB

```

\


Significant reduction in size of docker image can be observed in above output.

\


\
