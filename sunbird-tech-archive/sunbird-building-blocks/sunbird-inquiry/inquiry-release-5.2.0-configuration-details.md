---
icon: elementor
---

# inQuiry--Release-5.2.0-Configuration-details

**Configuration Added:**

* Please check the configuration files and add below configuration.
* For variable information, Please refer to Variable Section.

**assessment-service:**

```
cloud_storage_container: "{{ cloud_storage_content_bucketname }}"

cloudstorage {
  metadata.replace_absolute_path={{ cloudstorage_replace_absolute_path | default('false') }}
  metadata.list={{ cloudstorage_metadata_list }}
  relative_path_prefix="{{ cloudstorage_relative_path_prefix | default('CLOUD_STORAGE_BASE_PATH') }}"
  read_base_path="{{ cloudstorage_base_path }}"
  write_base_path={{ valid_cloudstorage_base_urls }}
}
```

Configuration File Link For Reference:

[https://github.com/project-sunbird/sunbird-devops/blob/release-5.2.0-inquiry\_RC1/ansible/roles/stack-sunbird/templates/assessment-service\_application.conf](https://github.com/project-sunbird/sunbird-devops/blob/release-5.2.0-inquiry\_RC1/ansible/roles/stack-sunbird/templates/assessment-service\_application.conf)

**async-questionset-publish:**

```
#Cloud Storage Config
    cloud_storage_type: "{{ cloud_service_provider }}"
    cloud_storage_key: "{{ cloud_public_storage_accountname }}"
    cloud_storage_secret: "{{ cloud_public_storage_secret }}"
    cloud_storage_endpoint: "{{ cloud_public_storage_endpoint }}"
    cloud_storage_container: "{{ cloud_storage_content_bucketname }}"
    cloudstorage {
      metadata.replace_absolute_path={{ cloudstorage_replace_absolute_path | default('false') }}
      metadata.list={{ cloudstorage_metadata_list }}
      relative_path_prefix="{{ cloudstorage_relative_path_prefix }}"
      read_base_path="{{ cloudstorage_base_path }}"
      write_base_path={{ valid_cloudstorage_base_urls }}
    }
```

Configuration File Link For Reference:

[https://github.com/Sunbird-inQuiry/data-pipeline/blob/58d52be036712eff2e90a3842a1885d36d4473a7/kubernetes/helm\_charts/datapipeline\_jobs/values.j2#L118](https://github.com/Sunbird-inQuiry/data-pipeline/blob/58d52be036712eff2e90a3842a1885d36d4473a7/kubernetes/helm\_charts/datapipeline\_jobs/values.j2#L118)

**questionset-republish:**

```
#Cloud Storage Config
    cloud_storage_type: "{{ cloud_service_provider }}"
    cloud_storage_key: "{{ cloud_public_storage_accountname }}"
    cloud_storage_secret: "{{ cloud_public_storage_secret }}"
    cloud_storage_endpoint: "{{ cloud_public_storage_endpoint }}"
    cloud_storage_container: "{{ cloud_storage_content_bucketname }}"
    cloudstorage {
      metadata.replace_absolute_path={{ cloudstorage_replace_absolute_path | default('false') }}
      metadata.list={{ cloudstorage_metadata_list }}
      relative_path_prefix="{{ cloudstorage_relative_path_prefix }}"
      read_base_path="{{ cloudstorage_base_path }}"
      write_base_path={{ valid_cloudstorage_base_urls }}
    }
```

Configuration File Link For Reference:

[https://github.com/Sunbird-inQuiry/data-pipeline/blob/58d52be036712eff2e90a3842a1885d36d4473a7/kubernetes/helm\_charts/datapipeline\_jobs/values.j2#L164](https://github.com/Sunbird-inQuiry/data-pipeline/blob/58d52be036712eff2e90a3842a1885d36d4473a7/kubernetes/helm\_charts/datapipeline\_jobs/values.j2#L164)

Deprecated variables:

* sunbird\_cloud\_storage\_type
* sunbird\_public\_storage\_account\_name
* sunbird\_public\_storage\_account\_key
* azure\_public\_container
* sunbird\_content\_azure\_storage\_container
*

**Variables Added:**

* Below table has all variables and its default values present in the configuration file. Please override them with **values** as per the environment.

| **variable name**                     | **description**                                                                                                                      | **Default Value Given in the Configuration File**                                       | **service/job name which uses variable**                     |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| cloudstorage\_replace\_absolute\_path | Boolean value is required to enable/disable cloud storage agnostic urls in db.                                                       | false                                                                                   | assessment, async-questionset-publish, questionset-republish |
| cloudstorage\_relative\_path\_prefix  | String value is required. This value will be used as prefix for any metadata which holds cloud storage path                          | CLOUD\_STORAGE\_BASE\_PATH                                                              | assessment, async-questionset-publish, questionset-republish |
| cloudstorage\_metadata\_list          | Array of String value is required. This array will have list of metadata keys which holds cloud storage path                         | \["appIcon","posterImage","artifactUrl","downloadUrl","variants","previewUrl","pdfUrl"] | assessment, async-questionset-publish, questionset-republish |
| cloudstorage\_base\_path              | String value is required. The value could be either cloud specific base path or cname configured for current cloud storage provider. | "https://sunbirddevbbpublic.blob.core.windows.net"                                      | assessment, async-questionset-publish, questionset-republish |
| valid\_cloudstorage\_base\_urls       | Array of String value is required. This array will have list of all cloud path which should be accepted by service.                  | \["https://sunbirddevbbpublic.blob.core.windows.net"]                                   | assessment, async-questionset-publish, questionset-republish |
| cloud\_service\_provider              | String value is required. e.g: azure                                                                                                 | azure                                                                                   | async-questionset-publish, questionset-republish             |
| cloud\_public\_storage\_accountname   | String value is required.                                                                                                            | NA                                                                                      | async-questionset-publish, questionset-republish             |
| cloud\_public\_storage\_secret        | String value is required.                                                                                                            | NA                                                                                      | async-questionset-publish, questionset-republish             |
| cloud\_public\_storage\_endpoint      | String value is required. It could be empty string                                                                                   | NA                                                                                      | async-questionset-publish, questionset-republish             |
| cloud\_storage\_content\_bucketname   | String value is required.                                                                                                            | NA                                                                                      | assessment, async-questionset-publish, questionset-republish |
|                                       |                                                                                                                                      |                                                                                         |                                                              |

**Variables & Values For Sunbird-Ed:**

| **Variables**                         | **Value**                                                                               |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| cloudstorage\_replace\_absolute\_path | true                                                                                    |
| cloudstorage\_relative\_path\_prefix  | CONTENT\_STORAGE\_BASE\_PATH                                                            |
| valid\_cloudstorage\_base\_urls       | \["https://sunbirdstagingpublic.blob.core.windows.net"]                                 |
| cloudstorage\_metadata\_list          | \["appIcon","posterImage","artifactUrl","downloadUrl","variants","previewUrl","pdfUrl"] |
| cloudstorage\_base\_path              | "https://sunbirdstagingpublic.blob.core.windows.net"                                    |
| cloud\_service\_provider              |                                                                                         |
| cloud\_public\_storage\_accountname   |                                                                                         |
| cloud\_public\_storage\_secret        |                                                                                         |
| cloud\_public\_storage\_endpoint      |                                                                                         |
| cloud\_storage\_content\_bucketname   |                                                                                         |

***

\[\[category.storage-team]] \[\[category.confluence]]
