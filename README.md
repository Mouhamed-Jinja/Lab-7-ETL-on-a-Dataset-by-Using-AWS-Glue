# AWS Glue and Athena Lab

<img width="709" alt="glue_lab_after" src="https://github.com/Mouhamed-Jinja/Lab-7-ETL-on-a-Dataset-by-Using-AWS-Glue/assets/132110499/7198f2db-a850-4b30-aef1-31c7287b919f">

## Overview
This repository contains the steps to perform ETL on a dataset using AWS Glue and querying the data using Athena.

## Task 1: Using an AWS Glue crawler with the GHCN-D dataset

### Configure and create the AWS Glue crawler
1. Open the AWS Management Console and navigate to AWS Glue.
2. Under Databases, select Tables.
3. Click on Add tables using crawler.
4. Name the crawler "Weather" and keep the default settings for Tags.
5. Choose Add a data source and configure the following:
   - Data source: S3
   - Location of S3 data: In a different account
   - S3 path: s3://noaa-ghcn-pds/csv/by_year/
   - Subsequent crawler runs: Crawl all sub-folders
6. Choose Add an S3 data source.
7. For Existing IAM role, select "gluelab".
8. In the Output configuration section, choose Add database, name it "weatherdata", and create the database.
9. Select the weatherdata database.
10. In the Crawler schedule section, choose Frequency: On demand.
11. Review the crawler configuration and choose Create crawler.
12. Wait for the crawler status to change to Ready.

### Run the crawler
1. On the Crawlers page, select the Weather crawler.
2. Choose Run and wait for the status to change to Ready.

### Review the metadata
1. In the navigation pane, select Databases.
2. Choose the weatherdata database.
3. Click on the by_year table and review the metadata.

### Edit the schema
1. From the Actions menu, choose Edit schema.
2. Change the column names according to the provided table.
3. Choose Update schema.

## Task 2: Querying a table by using Athena

### Configure an S3 bucket for Athena query results
1. In the AWS Glue console, navigate to Tables under Databases.
2. Click on the by_year table and choose Actions > View data.
3. Proceed to the Athena console and select Settings.
4. Manage the Location of query result and choose the data-science-bucket.
5. Save the settings.

### Preview a table in Athena
1. Switch to the Athena Editor tab.
2. Set Data source to AwsDataCatalog and Database to weatherdata.
3. Choose the by_year table and select Preview Table to view the data.

### Create a table for data after 1950
1. Retrieve the bucket name containing glue-1950-bucket.
2. In the Athena query editor, execute the provided query replacing <glue-1950-bucket> with the bucket name.
3. Run the query and preview the results.

### Run a query on the new table
1. Create a view for the maximum temperature reading.
2. Run a query to calculate the average maximum temperature for each year.

## Task 3: Creating a CloudFormation template for an AWS Glue crawler

### Find the IAM role ARN
1. Navigate to the IAM console and select Roles.
2. Locate and copy the ARN for the gluelab role.

### Create a CloudFormation template
1. Open the AWS Cloud9 IDE and create a new file named gluecrawler.cf.yml.
2. Copy and paste the provided CloudFormation template into the file.
3. Replace <GLUELAB-ROLE-ARN> with the copied IAM role ARN.
4. Save the file and validate the template using the AWS CLI.

### Deploy the CloudFormation stack
1. Run the command to create the CloudFormation stack using the template.
2. Verify the stack creation and check the resources created.

## Conclusion
By following these steps, you can perform ETL tasks with AWS Glue, query the data with Athena, and automate the creation of Glue crawlers using CloudFormation.




