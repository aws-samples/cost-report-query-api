# AWS Billing API
This project contains source code and supporting files for exposing an API to pull billing information. The template deploys a Cost and Usage report, and associated resources for crawling the report and populating a Glue Database for Athena queries. The API Gateway endpoint exposes a GET method for querying information based on based on AccountID, Month and Year.

## Deployed resources

The project includes a cloud formation template with a Serverless Application Model (SAM) transform to deploy resources as follows:

## CUR Report Definition
- AWSStartCURCrawler

### AWS Lambda functions
- AthenaBillingFunction: Athena query.
- AWSCURInitializer:

## Glue
- AWSCURReportStatusTable: Glue Table
- AWSCURCrawler: Glue Crawler 
- AWSCURDatabase: Glue Database
### API Gateway
- accessAPI. API endpoint for message reception. 

### S3
- ReportsBucket. Bucket used for storing reports.

## Prerequisites.
1. AWS Console Access with administrator account.
1. Cloud9 IDE or AWS and SAM tools installed and properly configured with administrator credentials.

## Deploy the solution
1. Clone this repo.

`git clone https://github.com/aws-samples/aws-billing-api`

2. Build the solution with SAM.

`sam build` 

if you get an error message about requirements you can try using containers.

`sam build -u` 


3. Deploy the solution.

`sam deploy -g`

SAM will ask for the name of the application (use "billing-api" or something similar) as all resources will be grouped under it; Region and a confirmation prompt before deploying resources, enter y.
SAM can save this information if you plan un doing changes, answer Y when prompted and accept the default environment and file name for the configuration.

## Usage
1. Once deployed, you can invoke the API endpoint, which can be found under Lambda Applications. The endpoint should be appended with the AccountID, Month and Year parameters, such as the following:
    `https://<YOUR-API-ENPOINT>/Prod/test?AccountID=AAAAAAAA&Month=MM&Year=YYYY`

## Resource deletion
1. Empty the associated S3 bucket. 
1. Back on the cloudformation console, select the stack and click on Delete and confirm it by pressing Delete Stack. 
