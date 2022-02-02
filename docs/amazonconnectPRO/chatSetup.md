# Chat Setup


## Lambda Setup

### Adding layers

Select `layers` on the sidemenu and click `Create Layer` button

![create_layer](/images/create_layer.png)

Download the layer files from <a href="https://lambda-layers-1h8d3.s3.ap-south-1.amazonaws.com/freshdesk-integration-layer.zip" target="_blank">S3 link</a>

![layer_configuration](/images/layer_configuration.png)

Fillout the fields as required and upload the ZIP file which downloaded before. Select `Node 14.x` as runtime and create the layer.

Create new lambda function with basic execution permission with runtime `Node 14.x`  and copy the code from the <a href="https://github.com/Sandeza/AmazonConnectPRO-Installations/blob/master/chat/lambda" target="_blank">Github repo</a>.

> Note : Lambda and AWS Connect instance should be in same region

Add layers to lambda by selecting `Layers` under `Designer` tab and click `Add a layer` button as shown below

![add_layer](/images/add_layer.png)

Select the layer which you have created before and the layer version then click Add button

![select_layer](/images/select_layer.png)

Now the layer will get added to lambda as shown below

![layer_added](/images/layer_added.png)

Add the environment variables as shown in below image

> Note : Include `https://` in beginning and don't include `/` at last

![env_variables](/images/env_variables.png)


## Contact Flow Setup

As show in the below image create a contact flow in Amazon Connect. 

![chat_contactflow](/images/chat_contactflow.png)

Open the lambda block and select the lambda created in the previous steps and then change the Timeout to 8sec.

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

## Customer Chat Widget Setup 

To setup Customer side chat widget refer below: 

 - First, you need to create a stack in CloudFormation with the template from the below link.

GITHUB LINK : <a href="https://github.com/Sandeza/AmazonConnectPRO-Installations/blob/master/chat/chat-stack/chat-cloudformation-template">CloudFormation Template Chat</a>
<!-- GITHUB LINK: <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI">startChatContactAPI</a> and <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI#cloudformation-deployment-steps">CloudFormation Deployment Steps</a> -->

  
 - Once your stack is deployed, go to the API Gateway console, select the API, go to the Stages menu item, and select the Prod stage. You will then see the Invoke URL. This is the URL you will invoke to start the chat.
  
 - Gather the instance ID and contact flow ID you want to use.You can find these IDs when viewing a contact flow.
 - Download the <a href="https://github.com/Sandeza/AmazonConnectPRO-Installations/tree/master/chat">chat</a> and save it locally.
 - Open `index.html` file and change the `region`, `apiGatewayEndpoint` with the newly created API Gateway Endpoint, `contactFlowId`, `instanceId` from the previous steps
  
                     connect.ChatInterface.initiateChat({
                            name: customerName,
                            username: "user_" + customerName,
                            region: "xxxxxxx",
                            apiGatewayEndpoint: "xxxxxxxx",
                            contactAttributes: JSON.stringify({
                                "customerName": customerName,
                                "customerEmail": email
                            }),
                            contactFlowId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx",
                            instanceId: "xxxxxx-xxxx-xxxx-xxxxxxxxx"
                        }, successHandler, failureHandler)

 - At this point you can open the `index.html` to test chat by entering your Name and Phonenumber.
 - For creating you own Chat User Experience refer : <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI#creating-your-own-chat-ux">creating-your-own-chat-ux</a> 

  




