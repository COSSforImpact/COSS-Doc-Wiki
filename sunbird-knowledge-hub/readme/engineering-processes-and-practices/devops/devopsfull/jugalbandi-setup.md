---
icon: elementor
---

# Jugalbandi setup

## Code repos: <a href="#jugalbandisetup-coderepos" id="jugalbandisetup-coderepos"></a>

Main repo: [https://github.com/OpenNyAI/jugalbandi-api](https://github.com/OpenNyAI/jugalbandi-api)

Forked repos :

* [https://github.com/project-sunbird/jugalbandi-api](https://github.com/project-sunbird/jugalbandi-api)
* [https://github.com/vaibhavbhuva/jugalbandi-api](https://github.com/vaibhavbhuva/jugalbandi-api)
* [project-sunbird](https://github.com/project-sunbird/jugalbandi-api)
* [sunbird-certification](https://github.com/vaibhavbhuva/jugalbandi-api)

Docker setup:

*   Clone one of the forked repo , Ex:

    ```
    git clone https://github.com/vaibhavbhuva/jugalbandi-api
    ```
*   Update Dockerfile for these ENV vars with your details

    ```
    GOOGLE_APPLICATION_CREDENTIALS=YOUR_GCP_CREDENTIALS_JSON_FILE \ #should be in the current directory
    BUCKET_NAME=YOUR_GCP_BUCKETNAME \
    DATABASE_NAME=YOUR_JUGALBANDI_DB_NAME \
    DATABASE_USERNAME=YOUR_POSTGRES_DB_USERNAME \
    DATABASE_PASSWORD=YOUR_POSTGRES_DB_PASSWORD \
    DATABASE_IP=YOUR_POSTGRES_HOST \
    DATABASE_PORT=YOUR_POSTGRES_PORT \
    OPENAI_API_KEY=YOUR_OPEN_API_KEY
    ```
*   Docker build and run ex:

    ```
    sudo docker build -t jugalbandi-sc .  # change image name according to the project
    sudo docker run -d -p 9000:8000 --name jugalbandi-sc  jugalbandi-sc # update port binding as per the requirement
    ```
* Update the security group in Azure to open-up the desired port.
