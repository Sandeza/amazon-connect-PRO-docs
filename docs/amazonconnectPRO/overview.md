
# Overview 
Amazon Connect is an easy to use cloud contact center that helps you provide superior customer service. Amazon Connect provides a seamless experience across voice and chat for your customers and agents.


# Description

The Freshdesk Support Desk + Amazon Connect integration brings the power of Connect right within Freshdesk. Agents can now engage with their customers through Amazon Connect’s Call and Chat channels without having to move out of Freshdesk. The integration also gives additional context to agents in terms of previous chat, call or ticket histories raised in Freshdesk so that they can have more contextual and effective interactions. 

### The custom app has two parts 
####   (i) a small modal and
####   (ii) a full page app. 
####   The small modal allows basic call functionality including the following:

 - Accepting incoming calls and chats
 - Making outbound calls
 - Searching for numbers in call logs and contact lists
 - Saving unknown numbers into contacts module
 - Converting a call conversation to a ticket in Freshdesk
 - Adding notes related to a conversation
![FreshdeskCCP](/images/freshdeskccp.png)


### The full page app allows agents to extend their capabilities by:

 - Using Live Transcribe and Live Translate features
![fullpage_Transcribe](/images/fullpageapp1.png)

![fullpage_Transcribe](/images/fullpageapp2.png)

 - Connecting with customer through Chats
![fullpage_Transcribe](/images/fullpageapp3.png)


 - Making planned Auto-call outs to customers
![fullpage_Transcribe](/images/fullpageapp4.png)



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
