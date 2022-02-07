# Auto Callout Setup 

## Initial Setup
​
### Creating Dynamo DB Table
​
- Create a DynamoDB table with the name "callerData"
- Set "agentIdentifier" as Partition key and "jobKey" as Sort key.
​
​
### Creating Lambda's
​
Create 3 Lambda's AutoCaller, AutoCallout and CallerDetails from the link below

>Note: Create the lambdas with `python3.9` as runtime.
  
 Link: <a href="https://github.com/Sandeza/AmazonConnectPRO-Installations/tree/master/autocallout">Auto Callout lambda </a>
- Set environment variable for the lambda fd-AutoCaller with callerData as key and give the Dynamo DB table name as the value.
- Set environment variable for the lambda fd-AutoCallout with callerData as key and give the Dynamo DB table name as the value. 
- Set another environment variable for the lambda AutoCallout with sourceNumber as key and give the amazon connect phone number that will be used to make outbound calls.
- Set environment variable for the lambda fd-CallerDetails with callerData as key and give the Dynamo DB table name as the value.
​
### API Gateway
​
- Create a REST API with the name autoCall
- Create a resource called Call.
-  In that resource create a POST method.
- Select Integration type as Lambda Function and enable Lambda Proxy integration.
- Select the Lambda function AutoCaller, that we created before.
- In that resource create a GET method.
- Select Integration type as Lambda Function, this dosen't need Lambda Proxy integration.
- Select the Lambda function CallerDetails, that we created before.
- Deploy the API and copy the URL. 

### Auto Callout Contact Flow Setup
  
- Create a contact flow as show below 

![AutoCallout](/images/autocallout_contactflow.png)

- Copy the Auto Callout Contact Flow Id

### Installation Parameters

- Add the Auto Callout URL and Contact Flow Id to the Freshdesk installation settings as shown below
 
![AutoCallout](/images/installationparams.png)