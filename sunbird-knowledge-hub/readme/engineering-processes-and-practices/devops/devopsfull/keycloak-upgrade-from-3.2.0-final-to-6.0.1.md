---
icon: elementor
---

# Keycloak Upgrade from 3.2.0-Final to 6.0.1

Our Sunbird Uses Keycloak mainly for user authentication and as 3.2.0 has become obsolete we have upgraded from keycloak-3.2.0-Final to 6.0.1.

## Steps to be followed for migration. <a href="#keycloakupgradefrom3.2.0-finalto6.0.1-stepstobefollowedformigration" id="keycloakupgradefrom3.2.0-finalto6.0.1-stepstobefollowedformigration"></a>

* Trigger Core cassandra backup job.
* Build the keycloak from the keycloak-6 branch of [sunbird-auth](https://github.com/project-sunbird/sunbird-auth/tree/keycloak-6) repo.
* Run KeycloakMigration Jenkins job with below options.

```
absolute_job_path: ArtifactUpload/{env}/Core/Keycloak 
private_branch: {yourPrivateBranch} 
branch_or_tag: release-2.8.0
```

This Jenkins Job takes the backup of the keycloak postgres database and creates a new database in same postgres instance with prefix {keycloakDBName}\_301, after it takes the backup, it checks if monit is present in the system and stops it to make sure it won’t cause any issues which performing the migrations by starting the keycloak server. After the monit is stopped it will stop the keycloak servers and starts the migration process, after succesfull migration it starts back monit, if monit fails for some reason then don’t worry. But check if the migration was success by the jenkins console. If you find any issues with the migration then revert back to previous migration.

* After the migration is succesfull then deploy the keycloak-6 changes which you have build from sunbird-auth branch, make sure you provide the below jenkins parameters.

```
absolute_job_path: ArtifactUpload/{env}/Core/Keycloak
private_branch: {yourPrivateBranch}
sunbird_auth_branch_or_tag: keycloak-6
branch_or_tag: release-2.8.0
```

After the keycloak-6 is deployed verify your changes by logging in to the application or by tunneling into the app and seeing the updated UI of keycloak.

```
 ssh -L 8080:localhost:8080 username@{keycloakIpAddress}
```

If you want more information on the detailed steps on migration, do refer this [Link](https://project-sunbird.atlassian.net/wiki/spaces/UM/pages/1087504491/KeyCloak+6.0.1+upgrade#KeyCloak6.0.1upgrade-24March2020).
