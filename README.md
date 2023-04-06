## NYC Citibike-Data-Pipeline

### Overview:
This project has been developed as part of [2023 Data Engineering Zoomcamp](https://github.com/DataTalksClub/data-engineering-zoomcamp). The goal of the project is to implement NYC's Citibike data pipeline. Its a batch pipeline which extracts data from [here](https://s3.amazonaws.com/tripdata/index.html) and stores the raw data into gcs bucket and bigquery. Stored data from bigquery will be transformed using dbt and transformed dataset will be used by looker data studio to develop visualizations for analytics purposes.

### Citibike Pipeline Architecture:

![image](https://user-images.githubusercontent.com/10378935/229990884-bd4dc8d5-482d-4ff7-8f46-cc4f0ef6981b.png)


### Problem description:
Citi Bike is NYC’s official bike share program, designed to give residents and visitors a fun, affordable and convenient alternative to walking, taxis, buses and subways. Citi Bike think that biking is the best way to see NYC! It's a quick and affordable way to get all around the city, and it even allows you to sightsee along the way. 
Project answers the below questions and helps bikers to explore the NYC.
 
* Where do Citi Bikers ride? 
* Which stations are most popular? 
* What days of the week are most rides taken on? 
* What are the total number of trips?


### Dashboard examples: 
you can find the report [here](https://lookerstudio.google.com/s/lUSsqr0LbT4)

![image](https://user-images.githubusercontent.com/10378935/229953111-63b75134-806c-4ad3-8399-def09ed55ba4.png)



![image](https://user-images.githubusercontent.com/10378935/229953157-a526210d-293d-4ab6-aee4-afd5599f1706.png)



### Technologies:

Following technologies are used in implementing this pipeline

* Cloud: [Goggle Cloud Platform](https://cloud.google.com/)
  * Data Lake: [Goggle Cloud Storage](https://cloud.google.com/storage)
  * Data warehouse: [Google Big Query](https://cloud.google.com/bigquery)
* [Terraform](https://www.terraform.io/): Infrastructure as code (IaC) - creates project configuration for GCP to bypass cloud GUI.
* Workflow orchestration: [Prefect](https://www.prefect.io/)
* Data Transformation: [DBT](https://www.getdbt.com/)
* Data Visualisation: [Google Looker data studio](https://lookerstudio.google.com/u/0/navigation/reporting)


## Setup to run the project


1. Clone the  git repo to your system
   ```bash
   git clone <your-repo-url>
   ```

2. Install the neccesary packages/pre-requisites for the project with the following command

   ```bash
     pip install -r requirements.txt
    ```

3. Next you need to setup your Google Cloud environment
- Create a Google Cloud Platform project, if you do not already have one(https://console.cloud.google.com/cloud-resource-manager)
- Configure Identity and Access Management (IAM) for the service account, provide the following privileges: 
  * BigQuery Admin
  * Storage Admin 
  * Storage Object Admin
- Download the JSON credentials and save it somehwere you'll remember, which will be JSON key.
- Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/install-sdk)
- Configure the environment variable point to your GCP key(https://cloud.google.com/docs/authentication/application-default-credentials#GAC) and authenticate it using following commands
   ```bash
     export GOOGLE_APPLICATION_CREDENTIALS=<path_to_your_credentials>.json
     gcloud auth application-default login
    ```

4. Set up the infrastructure of the project using Terraform
- If you do not have Terraform installed you can install it from [here](https://developer.hashicorp.com/terraform/downloads) and then add it to your PATH
- Once donwloaded navigate to the terraform folder :
    ```bash
     cd terraform/
    ```

- then run the following commands to create your project infrastructure
     ```bash
      terraform init
      terraform plan -var="project=<your-gcp-project-id>"
      terraform apply -var="project=<your-gcp-project-id>"
     ```

5. Run python code in Prefect folder
- you have installed the required python packages in step 1, prefect should be installed with it. Confirm the prefect installation with following command

    ```bash
      prefect --version
    ```
- You can start the prefect server so that you can access the UI using the command below:
   ```bash
   prefect orion start
   ```
- access the UI at: http://127.0.0.1:4200/
- Then change out the blocks so that they are registered to your credentials for GCS and Big Query. This can be done in the Blocks options
- You can keep the blocks under the same names as in the code or change them. If you do change them make sure to change the code to reference the new block name
- Go back to the terminal and run:
    ```bash
     cd prefect/
    ```
- then run
    ```bash
     python citibike_data_pipeline.py
    ```
- The python script will then store the citibike data both in your GCS bucket and in Big Query

6. Running the dbt flow
- Create a dbt account and log in using dbt cloud [here](https://cloud.getdbt.com/)
- Once logged in clone the repo for use 
- in the cli at the bottom run the following command:
   ```bash
    dbt run
    ```
- this will run all the models and create the final dataset called "fact_citibike"


7. On successful run , the linage of fact_citibike looks as below :


<img width="1173" alt="image" src="https://user-images.githubusercontent.com/10378935/230152162-ca3e91d7-fa30-410c-b8c0-3a8794d74c69.png">




8. Visualization 
- You can now utilize the fact_citibike dataset and use it within Looker for visualizations.


