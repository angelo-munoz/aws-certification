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