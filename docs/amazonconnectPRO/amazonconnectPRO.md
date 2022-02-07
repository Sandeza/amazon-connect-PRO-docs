
# Overview 
Amazon Connect is an easy to use cloud contact center that helps you provide superior customer service. Amazon Connect provides a seamless experience across voice and chat for your customers and agents.


# Description

The Freshdesk Support Desk + Amazon Connect integration brings the power of Connect right within Freshdesk. Agents can now engage with their customers through Amazon Connect’s Call and Chat channels without having to move out of Freshdesk. The integration also gives additional context to agents in terms of previous chat, call or ticket histories raised in Freshdesk so that they can have more contextual and effective interactions. 

### The custom app has two parts 
####   (i) a Contact Control Panel 
####   (ii) a full page app. 
####   The CCP (Contact Control Panel) allows basic call functionality including the following:

 - Accepting incoming calls and chats
 - Making outbound calls
 - Searching for numbers in call logs and contact lists
 - Saving unknown numbers into contacts module
 - Converting a call conversation to a ticket in Freshdesk
 - Adding notes related to a conversation

### The full page app allows agents to extend their capabilities by:

 - Using Live Transcribe and Live Translate features
 - Connecting with customer through Chats
 - Making planned Auto-call outs to customers

# CALLS
#### The call functionality can be managed in the small modal as well as the larger full page app. The full page app allows agents to leverage the additional features that are at their disposal such as:

 - Get additional caller meta-date from Amazon Connect

 - Live Transcribe: Capture the live transcription of the customer conversation as the call is progressing. This transcription then automatically gets added to the ticket created post the call for reference.
  
 - Live Translate: Translate the transcription of the call into the language of choice for the agent. This allows agents to ensure that they fully understand the customer requests if they were made in a different language than the language the agent is proficient in. The custom app currently supports translation to French, German and Hindi but this can potentially work in any language that AWS Translate supports. 
  
 - Auto Call out: Agents or supervisors can now send out automatic calls to customers to notify them of matters of interest. This feature allows agents to trigger calls that can be placed to multiple customers at once with a message of choice. The message can be typed in and the custom app automatically converts it into speech and dials the customer with that message. 

# CHAT
#### Amazon Connect now has a chat channel in addition to the call channel. If customers prefer to converse with their businesses through chat then agents can now respond to these chats right from within Freshdesk. 

 - The custom app also fetches any previous call, chat or ticket records from the customer so that they can understand the issue and support the customer contextually. Chat conversations can also be converted into tickets, if the agent chooses to do so. 

 - An Agent can take upto 5 customer chats in parallel. 



#### NOTE: The custom app itself is free and there are no charges for integrating the app from the marketplace with Freshdesk. However there will be charges made into your AWS account based on the usage of AWS services such as Connect (call, chat etc), transcription, translations, text to speech and outbound call for Auto Callout . The customer can choose which of these features are required to be enabled during the installation process.

# Initial Setup

## Domain Whitelist

Open the AWS Connect instance setup page and go to `Application integration` tab then whitelist the following domains

> https://freshdeskccpv2.arta.sandeza.io \
> https://d3h0owdjgzys62.cloudfront.net \
> Your freshdesk URL **eg : https://sandeza-support.freshdesk.com**

## Lambda Setup

### Adding layers

Select `layers` on the sidemenu and click `Create Layer` button

![create_layer](/images/create_layer.png)

Download the layer files from <a href="https://lambda-layers-1h8d3.s3.ap-south-1.amazonaws.com/freshdesk-integration-layer.zip" target="_blank">S3 link</a>

![layer_configuration](/images/layer_configuration.png)

Fillout the fields as required and upload the ZIP file which downloaded before. Select `Node 12.x` as runtime and create the layer.

### Creating Lambda

Create new lambda function with basic execution permission with runtime `Node 12.x`  and copy the code from the <a href="https://github.com/Sandeza/arta-freshdesk-integration-lambda" target="_blank">Github repo</a>.

> Note : Lambda and AWS Connect instance should be in same region

Add layers to lambda by selecting `Layers` under `Designer` tab and click `Add a layer` button as shown below

![add_layer](/images/add_layer.png)

Select the layer which you have created before and the layer version then click Add button

![select_layer](/images/select_layer.png)

Now the layer was added to lambda as shown below

![layer_added](/images/layer_added.png)

Add the environment variables as shown in below image

> Note : Include `https://` in beginning and don't include `/` at last

![env_variables](/images/env_variables.png)

### Whitelist

Open the AWS Connect instance setup page and go to `Contact flows` tab then whitelist the created lambda

![env_variables](/images/lambda_whitelist.png)

## Contact Flow setup

As Shown in the below image add lambda and set contact attribute block.

![contact_flow](/images/contact_flow.png)

Open the lambda block and select the created lambda then change the Timeout to 8sec

![contact_flow](/images/lambda_config.png)

Open the Set contact attribute block and give same Destination key and Attribute as `customerInfo` and type as `External`

>Note : Dont't change Destination key and Attribute value

![contact_flow](/images/set_contact_attribute.png)

# Chat Setup

# Contact Flow Setup

As show in the below image create a contact flow in Amazon Connect. 

![chat_contactflow](/images/chat_contactflow.png)

Open the lambda block and select the same lambda used in initial setup then change the Timeout to 8sec.

![add_layer](/images/add_layer.png)

Open the Set Contact Attributes block add Destination type and Destination Attribute as `customerInfo` and type as `External`

![chat_setcontactattributes](/images/chat_contactattributes_customerinfo.png)

Select `Add another attribute` and add Destination type as `User Defined`, Destination Attribute as `Call Reason` and select use text and enter `Issue`

![chat_setcontactattributes](/images/chat_contactattributes_reason.png)

Select `Add another attribute` and add Destination type as `User Defined`, Destination Attribute as `FD_Priority` and select use text and enter `High`

![chat_setcontactattributes](/images/chat_contactattributes_priority.png)

save the contact flow and create a New contact flow (inbound) to handle chat disconnection.

Refer to the below image to setup Chat Disconnect contact flow and Publish it.  

![chat_setcontactattributes](/images/chat_disconnectflow.png)

Go to the previous contact flow and add a `set disconnect flow` block and select the chat disconnect flow which was published before. 

Set a working Queue Block and select the required queue.

Set Transfer to Queue Block.

Set Disconnect Flow block. 

# Customer Chat Widget Setup 

To setup Customer side chat widget refer below: 

GITHUB LINK: <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI">Customer Chat Widget Setup </a>

# Transcribe Setup

Complete the Amazon real time Transcription setup using the link below:

GitHub Link : <a href = "https://github.com/amazon-connect/amazon-connect-realtime-transcription"> Amazon real time Transcription setup </a>

## After completing the setup:

Create two lambda functions `customerTranscriber` and `agentTranscriber` using the deployment package.
  
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
- Create 3 lambda's connect_handler , disconnect_handler, on_message_handler using the given deployment packages.
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
   - Add the connection URL in the Freshdesk App Intallation parameter 




