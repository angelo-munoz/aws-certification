# End-User Computing

## Amazon Worklink
mobile devices securely access corporate data using AWS as pass-through. 
- SAML 2.0 support
- no data stays/cached on device
- session started/accessed via secure link
- no need for VPN
- via mobile app
- vector graphics rendering

Reference: https://aws.amazon.com/worklink/

## Appstream 2.0   

- Service for securely streaming individual applications
- differs from Workspaces: AppStream is for individual applications and WorkSpaces is for an entire environment for any use. 

References:
- https://aws.amazon.com/appstream2

## Amazon Workspaces
- Desktop as a service
- Supports Linux and Windows

## AWS Comprehend Medical
- Extract information from unstructured medical text data
- Uses Natural language processing

## Reducing Hospital Readmissions
- Send msg to S3, lambda trigger, SQS, Lambda, outbound to Amazon Connect which makes the outbound call
- See the [architecture diagram](https://d1.awsstatic.com/architecture-diagrams/ArchitectureDiagrams/reduce-hospital-readmissions-ra.pdf)

## Amazon Pinpoint
- customer engagement platform, outbound and inbound marketing communications service, using emails, SMS, push, voice or in-app messaging

## Alexa for business
- improve meeting room experience
- make employees more productive by enriching the alexa voice commands with business context like conference room, location, device available in the room, etc to support commands like "alexa, who booked this room?", "Alexa, book this room" or other commands. 
- supports custom commands
- integrates w employee calendar to support commands like "Alexa, join the meeting." 
![](https://d1.awsstatic.com/product-marketing/A4B/product-page-diagram-AlexaForBusiness_how-it-works.2d3a37c5a31a5358d01ed8538327743d99078324.png)

## Amazon Transcribe
- speech to text service

## Amazon Comprehend
- extract insights from text stored in S3
![](https://d1.awsstatic.com/Comprehend/Use-cases_Customer-analytics.93d8f858f529bec19d1899c9d8a5625d3989e621.png)

# Amazon Forecast
- ML service for forecasting financial and business outcomes

Reference: https://aws.amazon.com/forecast/#