# Security

## AWS Shield Advanced
- includes notifications for incoming Layer 3 or Layer 4 attacks such as SYN floods and UDP reflection attacks. Shield standard doesn't include notification. 

## Lightweight Directory Access Protocol (LDAP)
- authenticate to LDAP first, then broker service (Cognito), then STS (with the assumed role), to get temp creds, which the app uses to access the AWS resource (S3, etc). Authenticate first!