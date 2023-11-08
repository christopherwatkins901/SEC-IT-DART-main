# SentinelOne Alert Monitoring Script Documentation

## SentinelOne Alert Monitoring Script Documentation

### Overview

This GitBook Wiki provides comprehensive documentation for the Python script designed to monitor SentinelOne alerts and send notifications to Slack. The script also utilizes AWS DynamoDB to keep track of the last processed alert.

### Table of Contents

* Overview
* Metadata
* Dependencies
* Functionality
  * Lambda Handler
  * AWS Resources
* Usage
* Deployment
* Error Handling

***

### Metadata

* **Language**: Python
* **AWS Services**: Lambda, DynamoDB
* **Third-Party Libraries**: `requests`

***

### Dependencies

* Python 3.x
* AWS SDK for Python (Boto3)
* Requests library

***

### Functionality

#### Lambda Handler (`lambda_handler(event, context)`)

**Parameters:**

* `event`: AWS Lambda event object.
* `context`: AWS Lambda context object.

**Actions:**

1. Fetches the Slack Webhook URL from environment variables.
2. Retrieves the last alert ID from DynamoDB.
3. Queries the SentinelOne API for new alerts.
4. Processes and sends each new alert to Slack.
5. Updates the last alert ID in DynamoDB.

**Returns:**

* HTTP status code 200 if successfully processed alerts.
* HTTP status code 400 or 500 if an error occurs.

#### AWS Resources

**DynamoDB Table (`SentinelOne_Last_Alert`)**

* **Attributes**: `id` (Number)
* **Provisioned Throughput**: Read 1, Write 1

**IAM Role (`LambdaExecutionRole`)**

* **Policies**: Allows `PutItem` action on DynamoDB.

**Lambda Function (`InitializeDynamoDBTableFunction`)**

* **Runtime**: Python 3.8
* **Role**: `LambdaExecutionRole`

***

### Usage

The script is intended to be deployed as an AWS Lambda function. It will be triggered by specific events, query the SentinelOne API for new alerts, and send notifications to Slack.

***

### Deployment

1. Package the script along with its dependencies.
2. Deploy the AWS CloudFormation template to create the necessary AWS resources.
3. Set the Slack Webhook URL as an environment variable in the Lambda function.
4. Test the function to ensure it's working as expected.

***

### Error Handling

The script uses Python's logging module to log errors. It returns an HTTP status code and a message indicating the nature of the error.

***
