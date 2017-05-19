# ts-lambda-pipeline
## Description
Compile AWS Lambda function with TypeScript to one with JavaScript and finally deploy it.

## System Requirement
* Globally installed [node](https://nodejs.org/en/)
* Globally installed [AWS Command Line Interface](http://docs.aws.amazon.com/ja_jp/cli/latest/userguide/installing.html)

## Installation
```
$ git clone https://github.com/tadasho/ts-lambda-pipeline.git
$ cd ts-lambda-pipeline/
$ npm install
```

## Set up
Rewrite ```[FUNCTION_NAME]``` at package.json , line 13
* If you don't have Lambda Function yet, configure and rewrite the 13th line of package.json
```
"build:lambda": "aws lambda create-function \
--region us-east-1 \
--function-name   CreateTableAddRecordsAndRead  \
--zip-file fileb://file-path/app.zip \
--role execution-role-arn \
--handler app.handler \
--runtime nodejs6.10 \
--vpc-config SubnetIds=comma-separated-subnet-ids,SecurityGroupIds=default-vpc-security-group-id \
--profile adminuser"
```
Reference:
- [Making Lambda Fuction](http://docs.aws.amazon.com/ja_jp/lambda/latest/dg/with-userapp-walkthrough-custom-events-upload.html)
- [CreateFunction](http://docs.aws.amazon.com/ja_jp/lambda/latest/dg/API_CreateFunction.html)

## How to use
1. Edit /src/index.ts
2. ```$ npm run build```

* * *

## About sample program
This TypeScript program is slack bot using AWS Lambda to receive events and respond to specific messages.

It looks for the words aws and lambda. If found, it will respond by mentioning the sender and giving Lambda praises.

### How to configure
1. Make [Slack API App](https://api.slack.com/apps?new_app=1) of your Slack team
2. Create an AWS Lambda Function and API Endpoint referring to [this](https://api.slack.com/tutorials/aws-lambda)
3. Uncheck the checkbox for ```API Gateway: Resources > /slack > POST > Integration Request > Use Lambda Proxy integration```
4. Handle events from the Events API using AWS Lambda referring to [this](https://api.slack.com/tutorials/events-api-using-aws-lambda)

### Try example
Let's type "aws" or "lambda" at your slack team !!
