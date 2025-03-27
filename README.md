# NBA-Data-Lake
This is a python script that automates the creation of a data lake for NBA analytics using AWS services. The script integrates Amazon S3, AWS Glue, and Amazon Athena, and sets up the infrastructure needed to store and query NBA-related data.

## Features 
- Fetches the NBA Player Data using sport data api
- Creates an S3 bucket to store the raw and processed NBA Data
- Creates an AWS Glue Dataase and an external table for querying the data
- Creates an AWS Athena for querying the data stored in the s3 bucket

### Additional Features
- Creates an AWS Glue ETL job on AWS Console to extract, transform, load the updated data to S3 bucket. 
- Creates an AWS Macie to scan, monitor and protect sensitive data in my S3 bucket

## Prerequisites
- AWS Account
- AWS CLI
- IAM User Account for access keys and secret keys
- IAM Role/Permission: Ensure the user or role running the script has the following permissions:

    - S3: s3:CreateBucket
    - S3:PutObject, 
    - s3:DeleteBucket, 
    - s3:ListBucket Glue: glue:CreateDatabase, glue:CreateTable, glue:DeleteDatabase, glue:DeleteTable Athena: athena:StartQueryExecution, athena:GetQueryResults
- SportDataIO Free Trial Account

## How To Run
1. Clone the Repository
Run the folloowing command to clone the repository:
```bash
git clone https://github.com/Franklyn-dotcom/NBA-Data-Lake.git
```

2. Configure AWS Credential in the CLI
After installing the AWS CLI, You need to configure your AWS CLI to enable you to connect and access your account. Run the following command to connect your aws account:
```bash
aws configure
```
You need to update the following with your credentials:
<quote>
AWS-ACCESS-KEY: #YOUR ACCESS KEY
AWS-SECRET-KEY: #YOUR SECRET KEY
AWS-REGION: #YOUR REGION HERE
</quote>

3. Create a virtual environment(venv)
After configuring your AWS CLI, You need to create a virtual environment(venv) for Python to enable you to manage separate package installations. Run the following command to create a virtual environment:
```bash
    python -m venv <name-of-your-virtual-env-folder>
```
To activate the virtual environment in Windows(powershell). Run the following command:
```bash
.\venv\Script\Activate.ps1
```

4.Install Packages 
After activating the virtual environment. Run the following command to install the packages using the *requirement.txt* file:
```bash
pip install -r requirements.txt
```
![requirement](/Images/end-of-requirement.png)

5. Running the script
Run the following command to run the script:
```bash
python src/nba-data.py
```
![show-script](/Images/running-script-success.png)

You should see the following output:
![s3-output](/Images/s3output.png)
![s3-obj](/Images/s3-obj.png)
![s3-obj-obj](/Images/s3-obj-obj.png)
![glue-db](/Images/glue-db.png)
![glue-db-table](/Images/glue-db-table.png)
![edit-athena](/Images/edit-athena.png)
You can query your data in the AWS Athena query editor. Run the following code in your query editor:
```sql
SELECT FirstName, LastName, Position, Team
FROM nba_players
WHERE Position = 'PG';
```
You should see the following output:
![show-athena](/Images/show-athena.png)
![view-athena](/Images/view-query.png)

## Further Enhancement / Additional Features
As an additional (non challenge) feature, I created a folder in the S3 bucket named Update-data-lake and an AWS Glue ETL Job to transfrom the data using the change scheme tool in the AWS Glue ETL Transfrom catalog to select only the necessary data i needed to query and stores the updated query data in the S3 folder. Also I created an AWS Macie to be able to scan and detect sensitive data in the S3 bucket

![glue-etl](/Images/glue-etl.png)
![glue-etl-view](/Images/glue-etl-view.png)
![s3-update-obj](/Images/s3-update-obj.png)
![s3-update-obj-obj](/Images/s3-update-obj-obj.png)
![macie-setup](/Images/macie-setup.png)
![process-macie](/Images/process-macie.png)
![macie-job](/Images/macie-job.png)
![macie-sucess](/Images/success-macie-scan.png)

## Resource
- [AWS Macie](https://www.youtube.com/watch?v=weV5JvX-lgo)
- [SportData IO API](https://sportsdata.io/)
- [AWS Glue Documentation](https://docs.aws.amazon.com/glue/)

