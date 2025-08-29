# Azure Data Factory 

- ADF managed service in the cloud for scale-out serverless data integration, data transformation and orchestration 
  - Azure data factory is PaaS service , so we don't requried to manage the patching , upgrading, maintaining and provisioning infrastructure on cloud and on-premises etc and there is no upfront costs. 
### Architectural Pattens for Analytics

 -  Ingest layer: 
    -  This is where we collect source data from diff sources and formats.We can get Structured data from an On-premise Database.We can get semi-structured data like CSV, JSON files. 
 - Store / Process layer : 
    - Stores the Ingested data in Azure data lake Gen2 Storage type
 - Enrich layer : 
    - We transform and enrich those processed data using Azure machine learning to apply ML Models on processed data.

   - We will refine, reshape the data for diff purposes like data warehouse and Machine Learning.
- Serve layer : 
   -  We can serve data for diff purpose for diff users and apps.
   - We can use Power BI to create dashboards and create reports on the data,
   - We can use Azure data share to share the data with external parteners.

![alt text](image.png)


### Architecture of hands-on project :

![alt text](image-1.png)

#### 

 1. Landing - The data arrive to this containers.
Just drop data as it is. No changes.

2. Raw - The raw data like json and csv file will be stored here without process.
Data is still unstructured but you organized it by folders, date etc.

3. Cleansed - Cleaned, stores Unique data and remove duplicates.
we will process the data from cleansed contianer into a staging layer within Azure SQL DB.

4. Curated Layer: In this final stage, the data is aggregated, joined, and modeled for a specific purpose. It's now ready for consumption.

Staging layer (Azure SQL DB)

Before holding into the data warehouse, data is stored in staging area where:
Temporary holding place for data
Used for validation, consistency check,
Make sure data is clean before final load to warehouses like Azure SQL DB

- the final data warehouse DWH. from this DWH we can serve the data for end user and applications via creating dashboard by Power BI.

- For delta lake, we will process the data from staging layer and bring it into Curated container in a delta lake formate using Azure Databricks.The delta lake supports for transactions like a DB.

- We will serve the data to end user via dashboards using Power BI.

- Azure Data Bricks for build the delta lake structure in azure delta lake storage Gen2

- Azure Data Factory - For Data pipeline and Orchestrations.

- Azure Data lake storage Gen2 - for Store the lot of data from multiple Data Sources.

- Azure SQL DB - For data warehouse


- created storage account with Enabled hierarchical namespace
![alt text](image-2.png)

- created azure SQL database 
  ![alt text](image-3.png)

- created azure data factory 

![alt text](image-4.png)


#### building a data pipeline

 #####  main components of data factory :

 1. Pipelines : logical grouping of activities needed to process.
 - The data pipeline can have one or more activities.
 - For example, we can have a pipeline consisting of a copy activity and a transform activity.

 2. Activities : Activities are the fundamental steps performing specific actions within a pipeline.

   - 3 types of activities 
      1. Data Movement Activities :Copy Activity to copy data from a source to a sink

      2. Data Transformation Activities : Change data – native Data Flows or External Service ex : filtering data , aggrigating data, change th eformate of the data 

      3. Data Control Activities : Logical control activities such as for each, conditions etc



 3. Linked Services :these are like connection strings that connect to our data sources. ex link data source to data set

 4. Datasets : The representation of the data that we work with is called a data set.

 5. Integration Runtime :  it is kind of the bridge between activities and linked services.

 6. Triggers :  triggers a kind of like switches to execute a pipeline.Pipelines can either be manually executed or by using a trigger.

![alt text](image-5.png)

- created two Container in  Storage account 1. landing 2. raw

![alt text](image-6.png)

- upload file in to landing Container
 ![alt text](image-7.png)

- creating pipeline in ADF
  ![alt text](image-8.png)
    - create new test connection and five storage account and subscription id and then test connection

    ![alt text](image-9.png)
   
    - than load file 

      ![alt text](image-10.png)

    - Destination data store : give Destination as a raw container

       ![alt text](image-11.png)
       ![alt text](image-12.png)

    - than go to monitor 

      ![alt text](image-13.png)   

      ![alt text](image-14.png)


     - now create new folder in pipeline and move created piline into folder 
      ![alt text](image-15.png)

     - now create new folder in datasets and move datasets  into folder 
     ![alt text](image-16.png) 

     - now created new container
       ![alt text](image-17.png)


     - now create new pipeline to copy data from raw container to cleansed  container

     ![alt text](image-18.png)


     ![alt text](image-19.png)
     ![alt text](image-20.png)
     ![alt text](image-21.png)  
     ![alt text](image-22.png)
     











