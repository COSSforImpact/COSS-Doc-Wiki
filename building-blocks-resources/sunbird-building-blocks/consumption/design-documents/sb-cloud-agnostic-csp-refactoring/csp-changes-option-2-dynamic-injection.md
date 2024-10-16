---
icon: elementor
---

# CSP Changes :: Option-2 ::Dynamic Injection

For each of the cloud providers we will have a NPM package and that will give us the specific cloud source object and configuration that needs to provided by the adapter&#x20;

For any frontend application, we need to add the specific cloud source provider’s npm package into the package.json and then we need to import the same class in the code.&#x20;



&#x20;

**Plan for breaking the cloud source provider is as follows:** \
Breaking _**Client-Cloud-Services**_  NPM package into individual cloud provider package and publish them&#x20;

\-_**@project-sunbird/azure-cloud-services**_&#x20;

_**-@project-sunbird/aws-cloud-services**_&#x20;

_**-@project-sunbird/gcp-cloud-service**_&#x20;

_**-@project-sunbird/sb-cloud-service**_ which will have the base class&#x20;

**For this we are using Jenkins build process as follows.**&#x20;

Changes in build scripts of portal to import the package dynamically during runtime based on input from Jenkins environmental variable&#x20;

1.  Changes in Jenkins file to get the value to new Jenkins  environment variable &#x20;

    ```
    stage('Build') {
      sh("bash ./build.sh  ${build_tag} ${env.NODE_NAME} ${hub_org} ${params.buildDockerImage} ${params.buildCdnAssests} ${params.cdnUrl} ${params.cloudProvider}")
    }
    ```
2. Changes in portal build scripts to dynamically change the imports of the cloud service provider in src/app/helpers/cloudStorage/index.js&#x20;

```
cloudProvider=$6

# function to run server build
build_server(){
    echo "Building server in background"
    echo "copying requied files to app_dist"
    cp -R libs helpers proxy resourcebundles package.json framework.config.js sunbird-plugins routes constants controllers server.js ./../../Dockerfile app_dist
    cd app_dist

    echo "Replacing the cloud provider in the code"
    cd helpers/cloudStorage

    IFS="@" read var1 var2 <<< "$cloudProvider"
    echo "var1=$var1, var2=$var2"
    echo $PWD

    sed -ie "s/[a-zA-Z]*-cloud-services/$var1/g" index.js

    cd ../..
    nvm use $NODE_VERSION
    echo "starting server yarn install"
    yarn install --no-progress --production=true
    echo installing the cloud provider ${cloudProvider}
    yarn install $cloudProvider
    echo "completed server yarn install"
    node helpers/resourceBundles/build.js -task="phraseAppPull"
}
```

**To make the code changes to the providers and make it generic from portal**&#x20;

3. Get the cloud service provider specific configuration from the NPM package in src/app/helpers/cloudStorage/index.js&#x20;

Eg: &#x20;

```
let cloudConfig = {
  provider: envHelper.sunbird_cloud_storage_provider,
  identity: envHelper.cloud_private_storage_accountname,
  credential: envHelper.cloud_private_storage_secret,
  reportsContainer: envHelper.cloud_storage_privatereports_bucketname,
  labelsContainer: envHelper.cloud_storage_resourceBundle_bucketname,
  region: envHelper.cloud_private_storage_region,
  projectId: envHelper.cloud_private_storage_project,
  endpoint:envHelper.cloud_private_storage_endpoint
};
```

4. Write a helper method to assign the values for these configurations from the devops environment variables directly in src/app/helpers/cloudStorage/&#x20;

```
const env = process.env
export const mapCloudConfig = (cloudConfig)=>{
    Object.keys(cloudConfig).forEach((item) => {
        cloudConfig[item] = env[item]
    })
    return  cloudConfig;
  }
```

5. Refactor the code in places to support generic environment variables&#x20;
