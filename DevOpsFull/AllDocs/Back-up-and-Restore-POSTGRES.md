Steps to take a backup of normal postgres vm and restore it to hosted service postgres:


1. Take the backup of roles and restore it to new postgres host by using below commands:

i. pg_dumpall -g > roles.sql

ii. psql --file=roles.sql --host=<ipaddress/dns_address of destination postgres> --port=5432 --username=<username>@<password> --dbname=postgres


1. Create the database with the owner on the new postgres host by using below command:

i. create DATABASE keycloak WITH OWNER=postgres;



Command to log in to hosted service postgres: psql --host=<ipaddress/dns_address of destination postgres> --port=5432 --username=<username>@<password> --dbname=postgres


1. Make the user(here we have user as sunbirddevnew) to member of role in new postgres host:

For example, if we are restoring the database called api_manager_dev then the user sunbirddevnew should be member of api_manager_dev role in the remote host.

Command:

GRANT "api_manager_dev" TO "sunbirddevnew";


1. Take the tables count on each databases before taking backup by running below query;

WITH rc(schema_name,tbl) AS ( select s.n,rowcount_all(s.n) from (values ('public')) as s(n) ) SELECT schema_name,(tbl).\* FROM rc;


1. Take the backup for each databases by using below command;

pg_dump -F p api_manager_dev > api-manager.sql


1. Run the restore command to restore the backup.



psql --file=/var/lib/postgresql/api-manager.sql --host=<ipaddress/dns_address of destination postgres>  --port=5432 --username=<username>@<password> --dbname=api_manager_dev


1. Verify the tables count on hosted service by using below query;

WITH rc(schema_name,tbl) AS ( select s.n,rowcount_all(s.n) from (values ('public')) as s(n) ) SELECT schema_name,(tbl).\* FROM rc;



*****

[[category.storage-team]] 
[[category.confluence]] 
