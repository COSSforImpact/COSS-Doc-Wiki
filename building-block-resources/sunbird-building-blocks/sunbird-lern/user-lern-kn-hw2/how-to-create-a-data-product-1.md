---
icon: elementor
---

# How-to create a Data Product

#### Python scripts <a href="#how-tocreateadataproduct-pythonscripts" id="how-tocreateadataproduct-pythonscripts"></a>

`cd` to python-scripts\
Step 1:  install virtualenv

```
pip install virtualenv
```

Step 2: create virtualenv

```
python -m virtualenv venv -p python3
```

step 3: activate virtualenv

```
source venv/bin/activate
```

step 4: build dataproducts lib

```
./build.sh
```

step 5: install the library

```
pip install bin/dataproducts.tar.gz
```

step 6: run the command

```
dataproducts user_declared_detail --data_store_location="/Users/kumar/projects/sunbird-data-products/reports" --states="dl,apekx"
```

Please setup the environment variables as follows

```
export PRIVATE_REPORT_CONTAINER="reports"
export REPORT_BACKUP_CONTAINER="portal-reports-backup"
export PUBLIC_AZURE_STORAGE_ACCOUNT=""
export PUBLIC_AZURE_STORAGE_ACCESS_KEY=""
```
