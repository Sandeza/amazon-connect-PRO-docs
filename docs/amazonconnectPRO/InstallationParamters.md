## Freshdesk Installation Parameters 

### Instance URL
Enter your Amazon Connect URL
>Note : If your Instance URL Ends with `.awsapps.com` append  `/connect `to the URL \
>Example: `https://sandeza.awsapp.com/connect` 
>If you Instance URL Ends with `.my.connect.aws` do not add `/connect` to the URL \
>Example: `https://sandeza.my.connect.aws`


### Instance Region
Enter the Region in which the Amazon Connect Instance is present. 
>Example: `us-east-1`

### Instance ID
Enter your Amazon Connect Instance ID.It can be found in the Instance ARN or within any ContactFlow under Addition Flow information section
>Example: `12345678-abcd-9112-a1b2-a1b2c3d4e5f6` 

### Freshdesk URL
Enter your Freshdesk URL 
>Note: Enter the Domain Name without `https` and `.freshdesk.com`

### Freshdesk APIKEY
Enter your Freshdesk APIKEY 


### Enable Transcribe
Enable this option to show the Transcriptions in the Fullpage App

### Enable Translate
Enable this option to show the Translation in the Fullpage App

### WebSocket URL
Websocket URL can be found in the API gateway service in your AWS account after completing the Transcribe Setup
> The URL's Protocol must be `wss`. \
>Example: `wss://transcribe-api.us-east-2.amazonaws.com/websocket`
### Enable AutoCallout 
Enable AutoCallout to show this feature in Fullpage App inside freshdesk 

### AutoCallout URL
Enter the AutoCallout URL that can be found inside API Gateway in your AWS Account after the AutoCallout Setup 
>Example:`https://autocallout-api.us-east-1.amazonaws.com/final/call`

### AutoCallout Contact Flow ID
Enter the AutoCallout ContactFlow ID from the Amaozn Connect ContactFlow which was created from AutoCallout Setup. 
>Note The Contact Flow id can be viewed inside the contact flow under Addition Flow information 
