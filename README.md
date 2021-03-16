# SNS -> S3 Logging

## Why

The reason behind this [AWS Lambda][1] function is to create a general-purpose function that can capture the payload of an Amazon SNS message and log it to an S3 bucket.


## How does it work?
[Amazon SNS][3] provides a mechanism for notifying interested subscribers of messages received on a topic. One of the subscriber types are is an AWS Lambda function.

This lambda function, once deployed, expects to be invoked by an SNS topic publish event. On invoking the function, the payload of the SNS message is inspected and written out to the S3 bucket defined in the `bucketName` environment variable of the function.

The flow is depicted below:

![AWS Lambda call flow](aws-lambda-flow.png)  

## Content
The source code is based on a NodeJS package structure and uses NPM to import libraries that facilitate certain core functions. The following are the key files needed:
- [src/lambda.js][2]: The lambda function to transform the payload
- [package.json](package.json): Defines the packaging tasks and the npm modules in use


## Requirements
- Need to create an [AWS account](http://docs.aws.amazon.com/lambda/latest/dg/setting-up.html)
- Need to setup [AWS CLI](http://docs.aws.amazon.com/lambda/latest/dg/setup-awscli.html) with the credentials of your AWS account
- NodeJS and NPM need to be installed


## Setting up the Components
The SAM template file, `template.yaml` defines the lambda to be deployed.  SAM will subscribe the lambda to the SNS Topic, and establish all IAM permissions to receive messages and write to the S3 bucket.


## Working with the source code
- Clone or fork this repository
- Ensure that you've followed the [Requirements](#requirements) section above
- ~~Run `npm run build` to install dependencies, package the Lambda function and node modules in a zip and finally deploys the Lambda function to AWS using the AWS CLI.~~
- Run `sam deploy --config-env {environment}`
  - environment parameters are configured in samconfig.toml

## License

See [LICENSE](LICENSE) for further details.



[1]: http://docs.aws.amazon.com/lambda/latest/dg/welcome.html
[2]: ./src/lambda.js
[3]: http://docs.aws.amazon.com/sns/latest/dg/GettingStarted.html
