---
cover: >-
  https://images.unsplash.com/photo-1509822929063-6b6cfc9b42f2?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwyfHxsb2dpbnxlbnwwfHx8fDE2OTg3MDg2MTJ8MA&ixlib=rb-4.0.3&q=85
coverY: 0
---

# Okta Audit logs 2 S3

## Okta Production Logging Script Documentation

### Overview

This GitBook Wiki provides comprehensive documentation for the Python script `okta-prod-logging.py`. This script is designed to collect Okta logs for compliance purposes and is part of Postman's production environment.

### Table of Contents

* Overview
* Metadata
* Dependencies
* Functionality
* Usage
* Deployment
* Contributors
* License

***

### Metadata

* **Author**: Christopher Watkins
* **Copyright**: Copyright 2023, Postman
* **License**: Apache License, Version 2.0
* **Version**: 1.0.0
* **Maintainer**: Christopher Watkins
* **Email**: christopher.watkins@postman.com
* **Status**: Production

***

### Dependencies

* Python 3.x
* AWS SDK for Python (Boto3)

***

### Functionality

#### `lambda_handler(event, context)`

**Parameters:**

* `event`: The event object containing details about the triggering event.
* `context`: The context object containing runtime information.

**Actions:**

1. Initializes the S3 client using Boto3.
2. Defines the S3 bucket name where the logs will be stored.
3. Converts the event object to a JSON-formatted string.
4. Defines the object key for the S3 bucket.
5. Uploads the JSON-formatted event to the specified S3 bucket.

**Returns:**

* HTTP status code 200 upon successful execution.
* A message indicating successful forwarding of Okta logs to S3.

***

### Usage

This script is intended to be deployed as an AWS Lambda function. It will be triggered by specific events, collect Okta logs, and store them in an S3 bucket for compliance purposes.

***

### Deployment

1. Package the script along with its dependencies.
2. Create a new AWS Lambda function and upload the package.
3. Configure the triggering events for the Lambda function.
4. Test the function to ensure it's working as expected.

***

### Contributors

* Christopher Watkins (Primary Maintainer)

***

### License

This script is licensed under the Apache License, Version 2.0. For more details, please refer to the [Apache License Documentation](https://www.apache.org/licenses/LICENSE-2.0).

***

