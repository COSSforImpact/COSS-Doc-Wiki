---
icon: elementor
---

# Offline-Consumption-of-QuML-Content

Solution

| **SQL Table** |                                                        |   |
| ------------- | ------------------------------------------------------ | - |
| Question Set  | Saves the metadata of Question Set in the table        |   |
| Question      | Saves the individual Question Metadata of the Question |   |

ECAR Structure

ECAR of Question Set

```
-------- metadata.json (Complete Question Set Hierarchy)

-------- do_id-1 (Question Leaf Folder)

                     ------ asset-1

                     ------ asset-2

                     ------ asset-3

                     ------ asset-4

     -------- do_id-2 (Question Leaf Folder)

                     ------ asset-1

                     ------ asset-2

                     ------ asset-3

                     ------ asset-4

     -------- do_id-2 (Question Leaf Folder)

                     ------ asset-1

                     ------ asset-2

                     ------ asset-3

                     ------ asset-4

……………    

……………

……………

……………

…………..



  -------- do_id-n (Question Leaf Folder)

                     ------ asset-1

                     ------ asset-2

                     ------ asset-3

                     ------ asset-4
```

ECAR Import Process :

1. Fetch the temporary Location from device
2.  Extraction of Ecar

    ```
     Unzip the Ecar using ZipService
    ```
3.  Validation of ECAR Content

    ```
     Absence of Manifest

     Invalid JSON in Manifest

      Empty JSON
    ```
4.  Extract Payload

    ```
     Copy the entire directory set on leaf nodes to File System of Device 
    ```
5. Update Size on Download Manager
6.  Create Manifest for each leaf node //Optional

    SQL Table

    Design 1: (Considering some limit is imposed on payload size)

    Question Set Table

\| do\_id (Primary Key) | Payload (Max Limit of 2 MB) | CreatedTime | UpdatedTime | | | | | |

```
   Design 2 : (Considering no limit is imposed on payload size)
```

Question Set Table

\| do\_id (Primary Key) | Spine Content (Max Limit of 2 MB) | CreatedTime | UpdatedTime | | | | | |

Question Table

\| do\_id (Primary Key) | Question Metadata | CreatedTime | UpdatedTime | | | | | |

Caching Strategy :

FIFO :

LIFO :

LRU :

***

\[\[category.storage-team]] \[\[category.confluence]]
