# SB-16478 - Load testing changes

#### SummaryAPI changesNew APIsChanged APIsInfra/config changes doneInfra/config changes attempted and revertedSummary <a href="#sb-16478-loadtestingchanges-summary" id="sb-16478-loadtestingchanges-summary"></a>

1. New APIs have been introduced with reduced payload.
   1. The reduction in request payload has helped remove data validation.
   2. The response has been cut to return only the required attributes pertaining to the operational intent.
2. In-memory cache is performed for roles now.
3. And configuration/operational changes in terms of memory has been increased.

#### API changes <a href="#sb-16478-loadtestingchanges-apichanges" id="sb-16478-loadtestingchanges-apichanges"></a>

**New APIs**

/v1/user/signup

/v1/user/exists/{idType}/{id}&#x20;

/v1/user/get/{idType}/{id} to get user details

Documentation: [https://github.com/project-sunbird/sunbird.org-docs/pull/551](https://github.com/project-sunbird/sunbird.org-docs/pull/551)

**Changed APIs**

Roles have been in-memory cached and returned instead of hitting db.

#### Infra/config changes done <a href="#sb-16478-loadtestingchanges-infra-configchangesdone" id="sb-16478-loadtestingchanges-infra-configchangesdone"></a>

1\. Cassandra write time out inscreased to 5000 from 2000 (write\_request\_timeout\_in\_ms)\
2\. Cassandra heap increased to 4GB\
3\. LMS ElasticSearch heap increased to 6GB\
4\. Added discovery.zen.minimum\_master\_nodes: 2 for ES - To avoid writes to ES in case one node goes down\
5\. Increase LMS ElasticSearch from 2 Core 14GB RAM, 6GB Heap (2GB initially) ==> TO ==> 4 Core, 16GB RAM, 8GB Heap\
6\. Postgres was restarted twice during load test activity due to 100% CPU usage and postgres being unresponsive\
7\. Keycloak Heap size increased from default 512MB to 6GB\
8\. Leaner service env variable for cassandra quoram was changed from QUORAM to LOCAL\_QUORAM\
9\. Added 3 IP's of ES and 3 Ports (9200) for learner service env. It was only 1 IP in env file\
10\. Upgraded ES LMS to 8 Core and 32GB RAM and 16GB Heap\
11\. Increase Postgres to 8 Core and then downsized it back to 4 Core\
12\. Changed keycloak password policy hashing from 20,000 to 1\
13\. Added 2 additional nodes for Keycloak - 2CPU, 8GB RAM (Total 4 VM's)\
14\. Created below indexes in Keycloak database on Postgres\
\- keycloak=> create index idx\_fed\_user\_credential\_type on fed\_user\_credential(type);\
\- keycloak=> create index idx\_fed\_user\_credential\_user\_id on fed\_user\_credential(user\_id);\
\- keycloak=> create index idx\_fed\_user\_attribute\_user\_id on FED\_USER\_ATTRIBUTE(user\_id);\
\- keycloak=> create index idx\_fed\_user\_attribute\_realm\_id on FED\_USER\_ATTRIBUTE(realm\_id);

#### Infra/config changes attempted and reverted <a href="#sb-16478-loadtestingchanges-infra-configchangesattemptedandreverted" id="sb-16478-loadtestingchanges-infra-configchangesattemptedandreverted"></a>

1\. Disabled brute force protection in Keycloak and later enabled it back - No difference - Reverted\
2\. Max connections in Keycloak - Tried 25 \*4, 50\*4, 100\*4. Did not see much difference in throughput. Reverted to default 100 per VM.\
3\. Removed require?ssl in keycloak - As there was no improvement, reverted to defaults, using ssl?require\
4\. Circuit breaker configuration in ES was updated 90% when we saw exceptions. But later was reverted to default to 70%\
5\. Changes keycloak connection-url value to use same as connection-property value - No difference - RevertedInfra / Config change to do:\
1\. Cassandra, ES, Keycloak to use automated calculation of heap size (OR provide variable for production override) - Keshav
