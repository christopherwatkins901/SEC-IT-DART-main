---
description: Sends Postman AWS Guard Duty Alerts to Slack
---

# Guard Duty 2 Slack

This documentation provides a comprehensive guide for understanding, deploying, and maintaining the GuardDuty-to-Slack Lambda function.

***

## GuardDuty to Slack Lambda Function

### Table of Contents

1. Introduction
2. Prerequisites
3. Architecture Overview
4. Setting Up the Environment
5. Python Version
   1. Code Explanation
   2. Deployment
6. Testing
7. Monitoring and Logging
8. Conclusion

***

#### Introduction

AWS GuardDuty is a threat detection service that continuously monitors for malicious or unauthorized behavior. The purpose of this Lambda function is to send alerts from AWS GuardDuty to a Slack channel, allowing for immediate action.

#### Prerequisites

* AWS Account
* Slack Workspace
* Basic knowledge of AWS Lambda, GuardDuty, and Slack webhooks

#### Architecture Overview

The architecture consists of three main components:

1. **AWS GuardDuty**: Monitors AWS environment for threats and generates findings.
2. **AWS Lambda**: Triggered by GuardDuty findings, processes the data, and sends it to Slack.
3. **Slack**: Receives alerts from Lambda via a webhook.

```
GuardDuty --(findings)--> Lambda --(alerts)--> Slack
```

#### Setting Up the Environment

**GuardDuty Setup**

1. Navigate to the GuardDuty console in AWS.
2. Click on "Enable GuardDuty".

**Slack Webhook Setup**

1. Go to your Slack workspace.
2. Create a new channel or choose an existing one for alerts.
3. Navigate to "Manage Apps" > "Custom Integrations" > "Incoming WebHooks" and set up a new webhook pointing to your chosen channel.

#### Python Version

**Python Code Explanation**

The Python version uses Boto3, AWS SDK for Python, and the `requests` library to send POST requests to Slack.

* **post\_message(message)**: Sends a POST request to Slack.
* **process\_event(event)**: Processes the GuardDuty finding.
* **lambda\_handler(event, context)**: Main Lambda function handler.

**Python Deployment**

1. Create a virtual environment and install `boto3` and `requests`.
2. Zip the Python code along with the installed packages.
3. Upload the zip file to your Lambda function in the AWS console.
4. Set environment variables for `webHookUrl` and `minSeverityLevel`.

#### Testing

To test the Lambda function:

1. Navigate to the Lambda function in the AWS console.
2. Use the "Test" feature to simulate a GuardDuty finding.

#### Monitoring and Logging

AWS CloudWatch can be used for monitoring and logging. Set up CloudWatch alarms to be notified about any issues with the Lambda function.

#### Conclusion

The GuardDuty-to-Slack Lambda function is a real-time alerting mechanism for AWS GuardDuty findings. It enhances security monitoring by sending immediate alerts to Slack, allowing for quick action to be taken.

***

