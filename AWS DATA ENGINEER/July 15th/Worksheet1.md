# AWS DATA ENGINEER PREPARATION 

## TOPICS FOCUSED ON TODAYS WORKSHEET
1. S3 BUCKETS
2. AWS GLUE

## S3 BUCKETS 

### WHAT IS AWS S3 ?

AWS S3 ( simple storage service ) is basically a object storage service provided by amazon web services . It basically helps to store and fetxh any amount of data anywhere from the web.
S3 can handle large amount of data and adjusts the data to accomodate our storage needs.

### WHAT ARE BUCKETS ?
S3 buckets are fundamental storage containers in Amazon S3 (Simple Storage Service) that are used to store and organize objects (files and their metadata). 
Each bucket has a unique name and serves as the top-level container for all the data you store in Amazon S3.

Here is how we create a bucket 

1. Create an AWS CONSOLE ACCOUNT
2. After registration Go to the AWS Console
3. Select The S3 SERVICES option


   <img width="741" alt="Screenshot 2024-07-15 at 9 37 27 PM" src="https://github.com/user-attachments/assets/32b69f9d-9861-4352-9284-9b195d74e29f">

4. Select the create bucket


   <img width="738" alt="Screenshot 2024-07-15 at 9 57 00 PM" src="https://github.com/user-attachments/assets/d054dea9-180c-48c2-8473-f7dfe4c5aced">


   HERE I HAVE NAMED MY BUCKET AS mudithinput1

5. Again I have created another bucket called mudithoutput1


   <img width="729" alt="Screenshot 2024-07-15 at 10 00 26 PM" src="https://github.com/user-attachments/assets/95ea5988-3a19-49bd-aa12-aaaa6a330f62">


   After creating both buckets the bucket dashboard was looking like this

   <img width="735" alt="Screenshot 2024-07-15 at 10 00 50 PM" src="https://github.com/user-attachments/assets/e5846e76-067f-416c-92c7-fd3c0e8bc596">

6. Aftfer clicking on the mudithinput1 here I am going to upload a csv file data into the input bucket

   <img width="724" alt="Screenshot 2024-07-15 at 10 09 46 PM" src="https://github.com/user-attachments/assets/df6328a2-1a6d-43d9-b020-696553bb33ef">

   Here Click on the upload

   <img width="726" alt="Screenshot 2024-07-15 at 10 15 57 PM" src="https://github.com/user-attachments/assets/f9b296dc-87fb-4ccc-9dd9-257611828394">


7.   <img width="724" alt="Screenshot 2024-07-15 at 10 17 54 PM" src="https://github.com/user-attachments/assets/27bf53c2-9dd5-438c-8153-27f2058d0cc6">


     Therefore This is how we Create buckets and upload a file into the bucket.
      

  ## AWS GLUE 

### WHAT IS AWS GLUE ?

AWS Glue is fully functional extract , transform and load ( ETL ) service provided by the amazon web services . It makes the data easy for simplification and it also automates the process of discovering , preparing the data for the tasks like analyics and application development.
The Main advantage of the AWS glue is that it is serverless it means we need not to manage any kind of Infrastructure.
There is something called Data catalog in AWS Glue where it acts as the central repository to store the metadata by making it easy to find and manage data.

### We will try to use the previously created buckets with AWS GLUE

1. We need to Create a crawler

 <img width="1000" alt="Screenshot 2024-07-15 at 10 27 01 PM" src="https://github.com/user-attachments/assets/c87f7866-7ac1-4728-bdf5-e25bf7d10a1f">


 ### What does a crawler do ?

In AWS Glue, a crawler is a component that automates the process of discovering and cataloging data stored in various data sources. 
The primary purpose of a crawler is to create or update the metadata tables in the AWS Glue Data Catalog.

### What is Meta Data ?

In AWS Glue, metadata refers to data that describes other data. This includes information about the structure format and organization of the data stored in various data sources.


2. Setting up the crawler properties
   <img width="1436" alt="Screenshot 2024-07-15 at 10 48 05 PM" src="https://github.com/user-attachments/assets/8f3cb508-6541-4fa2-a78a-9c646a5fcc7b">

   I have Mentioned a crawler name as projectaws
   
   <img width="776" alt="Screenshot 2024-07-15 at 10 51 01 PM" src="https://github.com/user-attachments/assets/fe14fc67-3e26-4467-9351-7afcdfe674cf">

   and after that I have added the data source , I have chosen the path from the previously Generateed buckets.

   <img width="648" alt="Screenshot 2024-07-15 at 10 51 25 PM" src="https://github.com/user-attachments/assets/e797d9db-c4b0-475d-977b-2c8b6ea7374e">

   This is How I mentioned the Source Path

   <img width="721" alt="Screenshot 2024-07-15 at 10 54 28 PM" src="https://github.com/user-attachments/assets/f58c37cf-6088-49b1-9aad-c0b4c3912cb8">

  After selecting the designated path I have Clicked onto the Next button

   <img width="627" alt="Screenshot 2024-07-15 at 10 54 51 PM" src="https://github.com/user-attachments/assets/d08a00c8-d31c-4b4d-9c78-34ef3b5c7b33">

   <img width="730" alt="Screenshot 2024-07-15 at 10 55 25 PM" src="https://github.com/user-attachments/assets/e4c2d6e9-d934-4e87-acbd-7da2067f7ea7">

   Creating an IAM ROLE 

   ### what is an IAM ROLE ?

   An IAM  Identity and Access Management role is an AWS identity with specific permissions that defines what actions are allowed and permitted or denied for specific AWS resources.

   I have created an IAM ROLE namely AWSGlueServiceRole-1 
   
   <img width="753" alt="Screenshot 2024-07-15 at 10 56 17 PM" src="https://github.com/user-attachments/assets/f808c2a7-62bc-492e-b64e-5dd58fc35209">

   <img width="722" alt="Screenshot 2024-07-15 at 10 56 34 PM" src="https://github.com/user-attachments/assets/951c5539-1243-4cce-9c01-0e66213d87a1">

   I Have created a DB named as mudithdb and I have added it to the Target Data Base 

   <img width="726" alt="Screenshot 2024-07-15 at 10 58 02 PM" src="https://github.com/user-attachments/assets/7ca9606a-8141-416e-a5ed-04458d61863a">

   <img width="727" alt="Screenshot 2024-07-15 at 10 59 40 PM" src="https://github.com/user-attachments/assets/0bc1470b-45a9-4023-8891-3854eb8f4d39">

   I have Checked initial crawler properties , data sources and Classifiers and I have configured The Database after all these steps I have clicked create crawler.

   <img width="734" alt="Screenshot 2024-07-15 at 11 00 02 PM" src="https://github.com/user-attachments/assets/84143d37-bc5c-4904-9c41-39c37ff7c121">

   Thus a Crawler in the AWS Glue is created 

   <img width="1422" alt="Screenshot 2024-07-15 at 11 00 29 PM" src="https://github.com/user-attachments/assets/d8bef8de-bd96-480b-84c5-0beb965e912d">



   

   


   

   
   
