# Data Ingestion API


### Project Setup
This project was created using the serverless framework and configured to use the serverless-offline plugin for local development

```bash
# Run serverless command to init project
$ serverless

Creating a new serverless project

# Select the AWS Node.js HTTP API starter project
? What do you want to make? (Use arrow keys)
  AWS - Node.js - Starter 
❯ AWS - Node.js - HTTP API 
  AWS - Node.js - Scheduled Task 
  AWS - Node.js - SQS Worker 
  AWS - Node.js - Express API 
  AWS - Node.js - Express API with DynamoDB 
  AWS - Python - Starter 
  AWS - Python - HTTP API 
  AWS - Python - Scheduled Task 
  AWS - Python - SQS Worker 
  AWS - Python - Flask API 
  AWS - Python - Flask API with DynamoDB 
  Other 

# After Serverless project is initialized

# initialize NPM
$ npm init


# After NPM is inintialized, install dependencies

# install serverless-offline
$ npm i serverless-offline

# install aws-sdk
$ npm i aws-sdk
```



## Adding the scheduled job to the serverless.yml

The following configuration was added to serverless.yml, which specifies a scheduled run of once a day

```yaml
  scheduledJob:
    handler: handler.scheduledJob
    timeout: 900
    events:
      - schedule: rate(1 day) # run every day
```



## Adding DynamoDB resource

[Documentation to work with DynamoDB in NodeJs](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/DynamoDB.html)

[Documentation to configure DynamoDB using CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-dynamodb-table.html)


The following configuration was added to create a sample DynamoDB database in the resources section

```yaml
    SomeTable:
      Type: "AWS::DynamoDB::Table"
      Properties:
        AttributeDefinitions:
        - AttributeName: "primaryId"
          AttributeType: "S"
        - AttributeName: "otherAttribute"
          AttributeType: "S"
        KeySchema:
        - AttributeName: "primaryId"
          KeyType: "HASH"
        BillingMode: PAY_PER_REQUEST
        TableName: SomeTableName
```



## Adding SecretsManager resource

[Documentation to work with SecretsManager in NodeJs](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/SecretsManager.html)

[Documentation to configure SecretsManager using CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-secretsmanager-secret.html)

The following configuration was added to create a SecretsManager resource


```yaml
    SomeSecret:
      Type: AWS::SecretsManager::Secret
      Properties:
        Name: SomeSecret
        Description: 'This is a secret that can be managed in AWS'
```
