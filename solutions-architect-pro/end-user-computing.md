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

**References:**
- https://aws.amazon.com/appstream2

## AWS Comprehend Medical
- Extract information from unstructured medical text data
- Uses Natural language processing

## Reducing Hospital Readmissions
- Send msg to S3, lambda trigger, SQS, Lambda, outbound to Amazon Connect which makes the outbound call
- See the [architecture diagram](https://d1.awsstatic.com/architecture-diagrams/ArchitectureDiagrams/reduce-hospital-readmissions-ra.pdf)

## Amazon Pinpoint
- customer engagement platform, outbound and inbound marketing communications service, using emails, SMS, push, voice or in-app messaging