<style>
    note { 
        border: 1px solid #3bf;
        padding: 1em; 
        display: block;
        margin: 0.5em;
        /* background-color: #4af;*/
        border-radius: 0.5em;
        prefix: "Note: "
    }
</style>
# IAM

## PARC model
- Principal. The requesting user or role
- Action. The verb to perform
- Resource. The target resource to perform the action on. 
- Condition. The conditions under which to perform this action. Ex: IP address, date period, etc.

## Principal
- User or role. 
- Service principal. AWS Organizations use trusted service principals

## AWS Organizations
- Service control policy (SCP) types: approve/deny policies
  - approve: whitelist. you approve max services accounts can access. everything else not allowed
  - deny: blacklist. you deny services accounts can access. everything else approved. 
- SCP's don't apply to management (master) accounts, or service-linked roles
- SCP's apply to all member account users, including root accounts
- Orgs integrate with stack sets for cross-region automation
- Benefits: consolidated billing, centralized account mgmt, centralized security
- AWS Quotas integration
- Use trusted service principals to allow services to access your organization or perform work on its behalf
- To exclude reserved instances, in billing console, add the account to the excluded reserved instances sharing

SCP exceptions: 
- Only **accounts** created after Sept 15, 2017 can control these actions with SCP's. That is, accounts before this date cannot control these actions with SCP's: 
    - Enable or disable multi-factor authentication on the root user
    - Create, update, or delete x.509 keys for the root user
    - Change the root user's password
    - Create, update, or delete root access keys
- SCP's can only have 1 statement object. Consolidate into an array as needed. 


References
- [Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
- [Establishing your best practice AWS environment](https://aws.amazon.com/organizations/getting-started/best-practices/)
- [Best Practices for Organizational Units with AWS Organizations](https://aws.amazon.com/blogs/mt/best-practices-for-organizational-units-with-aws-organizations/)


## IAM Identity Providers
Provides federated access to AWS Resources. Same concept as [Cognito Identity Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html) and Cognito Identity pools use IAM Identity providers under the hood. The difference is [use Cognito for web and mobile apps](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_federated-users.html#id_roles_common-scenarios_federated-users-cognito). 

Setup following the same conceptual steps as Cognito Identity pools, only Cognito Identity pools automates a couple steps that are manual in the IAM Identity providers. ex: creating the roles. 

Conceptual steps: 
1. Create the IdP connection
2. Create a role that federated users will assume. 
3. Configure trust bw IdP and Identity Provider. <note>💡 Note: Built-in with Cognito IdP</note>
4. Configure IAM policy that the role will use

<note>💡Note: Cognito Identity pools has concept of unauthenticated roles</notes>

References: 
- [IAM Identity Providers](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html)
- [Cognito Identity Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html)

## Federated Console access with google
Federate access to the AWS Console following these steps:
1. [Create google app](https://developers.google.com/identity/protocols/oauth2/openid-connect)
2. Configure 
3. Test

## Cross-account Access
- This is now a [legacy feature](https://aws.amazon.com/blogs/security/how-to-enable-cross-account-access-to-the-aws-management-console/) with the newer approach being to use [cross-account access by switching roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html) 

## IAM Policy types
- Identity. Defines the actions a user, or role can do across several resources. 
- Resource. Attach to resource (ex: S3) and specify which identities can perform specified actions

Sample policy: 
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid":"001",
      "Principal": "",
      "Effect":"Allow",
      "Action":"logs.*",
      "Resource":"*",
      "Condition":""      
    },
    {
      "Sid":"002",
      "Principal": "",
      "Effect":"Deny",
      "Action":"ec2.*",
      "Resource":"*",
      "Condition":""      
    }
  ]
}
```

References: 
- https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html

## Lightweight directory access protocol (LDAP)
- Open source
- lists users, printers and other directory items
- does authentication
- not encrypted in transit - needs TLS
- linked w [Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol)) for authentication 
- authenticate to LDAP first, then broker service (Cognito), then STS (with the assumed role), to get temp creds, which the app uses to access the AWS resource (S3, etc). Authenticate first!


![SSO w LDAP](https://media.tutorialsdojo.com/sap_sso_ldap.png)

## Security Assertion Markup Language (SAML)
- version 2.0 supported by AWS
- used for integration with identity providers
- supports SSO

## Single Sign-on (SSO)
- Uses SAML 2.0

## Federation
- authenticate by role, not user. Role trust policy must list the IdP as principal. 

## IAM Policy Evaluation Process
- Order of evaluation: 
  1. Authentication
  2. Determine resources
  3. Get Policies
  4. Determine access based on policies and resources
  
  See [Source](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html)


