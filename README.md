## NYC Citibike-Data-Pipeline

### Overview:



### Problem description:



### Technologies:

Following technologies are used in implementing this pipeline

* Cloud: **GCP**
  * Data Lake: **GCS**
  * Data warehouse: **Big Query**
* **Terraform**: Infrastructure as code (IaC) - creates project configuration for GCP to bypass cloud GUI.
* Workflow orchestration: **Prefect**
* Data Transformation: **DBT**
* Data Visualisation: **looker data studio**


### Citibike Pipeline Architecture:

![image](https://user-images.githubusercontent.com/10378935/229666445-7873dc6e-9314-43a0-9aa2-c01a3202e01a.png)



## Setup to run the project


1. Clone the repo and install the neccesary packages

```bash
pip install -r requirements.txt
```

2. Next you need to setup your Google Cloud environment
- Create a Google Cloud Platform project, if you do not already have one(https://console.cloud.google.com/cloud-resource-manager)
- Configure Identity and Access Management (IAM) for the service account, provide the following privileges: 
  * BigQuery Admin
  * Storage Admin 
  * Storage Object Admin
- Download the JSON credentials and save it somehwere you'll remember, which will be JSON key.
- Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/install-sdk)
- Let the environment variable point to your GCP key(https://cloud.google.com/docs/authentication/application-default-credentials#GAC), authenticate it.
