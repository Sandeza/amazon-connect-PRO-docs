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

GITHUB LINK: <a href="https://github.com/amazon-connect/amazon-connect-chat-ui-examples/tree/master/cloudformationTemplates/startChatContactAPI">Customer Chat Widget Setup </a>





