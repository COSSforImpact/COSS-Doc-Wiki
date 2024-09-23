 **In common.yml** 

ekstep_env: qa                                                                                                             # qa or dev or prod env of ekstep which you want ot connect

sunbird_content_repo_api_base_url: "[https://qa.ekstep.in/api](https://qa.ekstep.in/api)"                                    # qa or dev or prod env url of ekstep which you want ot connect

sunbird_analytics_api_base_url: [https://qa.ekstep.in/api](https://qa.ekstep.in/api)                                              # qa or dev or prod env url of ekstep which you want ot connect

sunbird_search_service_api_base_url: [https://qa.ekstep.in/api/search](https://qa.ekstep.in/api/search)                        # qa or dev or prod env url of ekstep which you want ot connect

sunbird_cloud_storage_urls: 'https://s3.ap-south-1.amazonaws.com/ekstep-public-{{ekstep_s3_env}}/,https://ekstep-public-{{ekstep_s3_env}}.s3-ap-south-1.amazonaws.com/'                                # This value can be same as this line

sunbird_ekstep_proxy_base_url: [https://qa.ekstep.in/](https://qa.ekstep.in/)                                                  # qa or dev or prod env url of ekstep which you want ot connect

upstream_url: "ekstep-public-{{ekstep_s3_env}}.[s3-ap-south-1.amazonaws.com](http://s3-ap-south-1.amazonaws.com)"      # This value can be same as this line

learningservice_ip:                                                                                                        # Dummy IP or provide IP of swarm manager

keycloak_auth_server_url: "{{proto}}://{{ proxy_server_name }}:8080/auth"                 # This value can be same as this line. If using a LB for keycloak, remove port :8080

 **In secrets.yml** 

core_vault_sunbird_ekstep_api_key:                                                                             # ekstep key

 **(After onboarding consumer take the value of api-management-test-user update the below variables)** 

core_vault_sunbird_api_auth_token:                                                                             # sunbird key after onboarding consumers

core_vault_kong__test_jwt:                                                                                            # sunbird key after onboarding consumers







*****

[[category.storage-team]] 
[[category.confluence]] 
