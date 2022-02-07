# Transcribe Setup

Complete the Amazon real time Transcription setup using the link below:

GitHub Link : <a href = "https://github.com/amazon-connect/amazon-connect-realtime-transcription"> Amazon real time Transcription setup </a>

## After completing the setup:

Create two lambda functions `customerTranscriber` and `agentTranscriber` using the deployment package.
>Note: Create the Lambdas using `Node 14.x` runtime

Link: <a href="https://github.com/Sandeza/AmazonConnectPRO-Installations/tree/master/transcribe">Transcribe lambda </a>
  
 - Set the following values for the environment variables :
  - WEBSOCKET_URL (The https URL of the webscoket we are going to create)
  - CONNECTION_DETAILS_TABLE ( Dynamo dB table name where contactId and connectionId of the websocket are stored )
  
Go to DynamoDB and open the `contactTranscriptSegments` and `contactTranscriptSegmentsToCustomer` Tables which was created by Cloudformation template
Select the table `contactTranscriptSegments` go to `Exports and Streams` and enable DynamoDB streams and select New and old images. 
  - Select Trigger and create a new Trigger
    - Select the Lambda `customerTranscriber`
Select the table `contactTranscriptSegmentsToCustomer` go to `Exports and Streams` and enable DynamoDB streams and select New and old images. 
  - Select Trigger and create a new Trigger
    - Select the Lambda `agentTranscriber`

# Websocket Setup
​
​
Websocket is used to stream transcription and translation from Amazon connect to freshdesk 
​

​
### Dynamo Db Table 
- Create a table "socketConnections" for storing the socket connections with hash as connectionId . 
- Create a table connectionDetails with Hash as ContactId and sort key as connectionId
### Lambda Creation
Create 3 lambda's `connect_handler`, `disconnect_handler` and `on_message_handler` using the given deployment packages.
>Note: Create the lambdas with Runtime `python 3.9`

 Link: <a href="https://github.com/Sandeza/AmazonConnectPRO-Installations/tree/master/transcribe/websocket">Websocket lambda </a>

- Set socketConnections table name for the environment variable SOCKET_CONNECTIONS_TABLE_NAME in connect_handler and disconnect_handler.
​
- Set connectionDetailstable name for the environment variable CONNECTION_DETAILS_TABLE_NAME in on_message_handler.
​
​
## Websocket creation
- Give a name for the websocket
- In the Add routes add connect route , disconnect route and default route
- Under the Custom routes add a new route with the name OnMessage
- In attach integrations attach the lambda functions we created to each route
- Create and deploy 
- Copy the websocket URL and connection URL
   -  Use the websocket URL as an environment variable in the `customerTranscriber` and  `agentTranscriber` Lambdas created in transcribeSetup

## Installation Parameters
- Add the connection URL in the Freshdesk App Intallation parameter 
  
![websocket_installation](/images/websocket_installationparams.png)
