---
icon: elementor
---

# Guide to Start and Stop Sunbird Ed environments

We have created jenkins jobs to start and stop the env which includes Kubernetes (AKS) cluster and Virtual machines in Azure

To start the environment, first start the virtual machines and then start AKS as databases need to be available for the application to start running otherwise it will end up with too many pod restarts

To stop the environment, stop the AKS cluster first and then stop the virtual machines where non-containerised workloads are runnning.

**How it works:**

We have created the service principle in azure which has access to start and stop the resources. Created Jenkins pipelines which leverages az cli commands to stop and start the resources using the service principle

You need to create job under OpsAdminstration Folder inside Jenkins(also you can create anywhere according to your usecase)

Jenkins pipeline to stop azure VM’s :

```
pipeline {
    agent any
    environment {
        SP_CRED = credentials('stag_az_sp')              // Azure SP credentials
        TENANT_ID = ""  // Azure Tenant ID to login
        RG = ""       // Azure Resource Group
        AZURE_CONFIG_DIR = "/var/lib/jenkins/Azure/Staging" // Azure config dir to store session
    }
stages {
    stage('Stop Azure VMs') {
        steps {
            script {
                sh 'az login --service-principal -u ${SP_CRED_USR} -p ${SP_CRED_PSW} --tenant ${TENANT_ID}'
                //sh "/usr/bin/az vm list -g $RG --query '[].id' -o tsv"
                sh 'az vm deallocate --ids $(az vm list -g  $RG --query "[].id" -o tsv)'
                }
                echo "All VMs in $RG have been stopped."
                echo "logging out"
                sh 'az logout'
            }
        }
    }
}
```

Jenkins pipeline to stop AKS cluster:

```
pipeline {

    agent any

    environment {

        SP_CRED = credentials('dev_az_sp')              // Azure SP credentials

        TENANT_ID = ""  // Azure Tenant ID to login

        RG = ""    // Azure Resource Group                           

        AZURE_CONFIG_DIR = "/var/lib/jenkins/Azure/Dev" // Azure config dir to store session                             

    }

  

    stages {

        stage('Start Azure AKS') {

            steps {

                script {

                    def AKS_CLUSTER = [ 'dev-k8s']

                    sh 'az login --service-principal -u ${SP_CRED_USR} -p ${SP_CRED_PSW} --tenant ${TENANT_ID}'

                    for (def aksName in AKS_CLUSTER) {

                    sh "az aks stop --name ${aksName} --resource-group ${RG}"

                    echo "$aksName is being stopped"

                    }

                    echo "logging out"

                    sh 'az logout'

                }

            }

        }

    }

}

```

Jenkins pipeline to start AKS cluster:

```
pipeline {

    agent any

    environment {

        SP_CRED = credentials('dev_az_sp')              // Azure SP credentials

        TENANT_ID = "4836227a-1ace-434f-b54c-8a7a14a0b449"  // Azure Tenant ID to login

        RG = "sunbird-devnew-env"    // Azure Resource Group                           

        AZURE_CONFIG_DIR = "/var/lib/jenkins/Azure/Dev" // Azure config dir to store session                            

    }

    

    stages {

        stage('Start Azure AKS') {

            steps {

                script {

                    def AKS_CLUSTER = ['dev-k8s'] // k8s Cluster Name which needs to start

                    sh 'az login --service-principal -u ${SP_CRED_USR} -p ${SP_CRED_PSW} --tenant ${TENANT_ID}'

                    for (def aksName in AKS_CLUSTER) {

                    sh "az aks start --name $aksName --resource-group ${RG}"

                    echo "$aksName is being started"

                    }

                    echo "logging out"

                    sh 'az logout'

                }

            }

        }

    }

}

```

Jenkins pipeline to start VM’s in a resource group:

```
pipeline {

    agent any

    environment {

        SP_CRED = credentials('dev_az_sp')              // Azure SP credentials

        TENANT_ID = "4836227a-1ace-434f-b54c-8a7a14a0b449"  // Azure Tenant ID to login

        RG = "sunbird-devnew-env"                                  // Azure Resource Group

        AZURE_CONFIG_DIR = "/var/lib/jenkins/Azure/Dev" // Azure config dir to store session   

    }

    

    stages {

        stage('Start Azure VMs') {

            steps {

                script {

                    sh 'az login --service-principal -u ${SP_CRED_USR} -p ${SP_CRED_PSW} --tenant ${TENANT_ID}'

                    sh 'az vm start --ids $(az vm list -g  $RG --query "[].id" -o tsv)'

                    }

                    echo "All VMs in $RG have been started."

                    echo "logging out"

                    sh 'az logout'

                    echo "sleep for 10 minutes for the VMs to start"

                    sh 'sleep 10m'

                }

            }

        }

    }
```

You can schedule these jobs as a cron from jenkins job configuration

Path for these Jenkins Jobs are under OpsAdministration/dev(your env name)/Core/

Screen Shots for setting up job

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXfim3PeksoUop-Jsq1TiKekcAFre4Gf-Y8F-4\_yr\_95MsZSemevyEbe5t04S6QwWgiOxpy3sU96Ypp0lzcFI7I2Zds5HDNSOpK0XpO4PnZMs2zqjumKd2H-cHUfIQgEWftFbZA96i3o2AyBovwFfOUvN6jo?key=OlAyu0X\_hc17UNM9EJP-PQ)

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXdVf\_ivh4Np16sqQKiW-RTITqXAATt\_SDbv9lT0\_NED67t\_N3QundtNSIKKqwWwSeMVyOc1jKkuwosS\_qdCevy9T5DIHlYLB2inKjBv53\_-xlQGfGLcG6ANxDrK\_g0APx5rbAPc1BU4md04OXpguGXxsZFn?key=OlAyu0X\_hc17UNM9EJP-PQ)![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcUV-fqjzY5MV6\_isTiw7b6IJ41xX6hmd6UFY0TuHQJCno12eCfVyTxuQ68SXmYpfgH-dve-HClX2j6Sn\_zBK9D9ZTPOctoiJTscEk24a5K7PGgmVij95mG54Op7hmueKO8ypH4rqWy2j3iv5j93IEtCkJ2?key=OlAyu0X\_hc17UNM9EJP-PQ)

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcEW4cMwtiJOLBiXBYukJhXKyHmcfcWHhUpywjPkWC9az5TFmRAmJFQNw0Sy07ZmF4dphCafOJY\_5fLpdgKPoLZxhYMDqdLmvWQs-94fBDKr-SZhTgSXVPFLxAHmaS\_AU57euIii-bwIomL\_z\_RIny9y-A?key=OlAyu0X\_hc17UNM9EJP-PQ)

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcbO-kYjNgk9FLlkwIKq92x6hlsiIzTf7gf3cOMP8bYjT6yaYEYf5FJksHMaPNyKcGTFBqC\_NGIq7Ql8LthQ576GTUTFCYw0KrS47lRToKaez18JKz00MabB6BLCwkozC2EYR2LgtsryA9lrXzKpQ4ddUo?key=OlAyu0X\_hc17UNM9EJP-PQ)![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXfzPtgMxobqKnnoSSmGtgusZ0gQ6-56f4lKViZjCCg-gzLcpAXkLhLUvmjEr\_zNvD7Rn-PTRjtIluf1dz8jjfTuPaeAu6hQJyZI4FUCDoqULUogbjAkCK8EXlww7vQPiwhUSKeU2AMjRirNqFT8QuDSAfc?key=OlAyu0X\_hc17UNM9EJP-PQ)

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXen5pOjbCzWE0mVYZ5UPjtyEPgv8a5zKCgS7L2navJMGHJICCRHtGA8XFsUUmSQUBPqTErcEWo8ieJTntfRqzJntXmB2TVmEr1qcGfuAWEUynJ4oFhnP3g\_fHLOiTpoVU9sWFhstfj-iSzwEITMY4ehtHs?key=OlAyu0X\_hc17UNM9EJP-PQ)

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXeMtVWIjIAX945-9oTdhLW2vN3SPqGt6i\_y5EfiTjvCK3hd-wm30-amr0seNjwntjvyfx9v0ZvWBnd6KeU-cASSRMLrVRYQcoQutrV0j3MYEdSu9cTyKhf6OmQkq-h3yEk--UWB5MjzcW3SNQk9aOLsT3U?key=OlAyu0X\_hc17UNM9EJP-PQ)
