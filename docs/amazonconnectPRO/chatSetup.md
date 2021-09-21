# Chat Setup

## Contact Flow Setup

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

## Customer Chat Widget Setup 

To setup Customer side chat widget refer below: 

 - First, you need deploy the backend API as instructed in the below links.
    
GITHUB LINK: <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI">startChatContactAPI</a> and <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI#cloudformation-deployment-steps">CloudFormation Deployment Steps</a>

  
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

  




