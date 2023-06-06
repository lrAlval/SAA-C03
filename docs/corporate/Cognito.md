![[Pasted image 20221031091542.png]]
# Amazon Cognito
>Cognito is a Server which grants and manager access to your applications running in AWS. This is archived by granting an authenticated user temporary [[IAM]] credentials.

## TLDR

## Sub Services

## User Pools
- Is a User directory
- You can use AWS build in user management or use external (google, twitter Facebook)
- You can use the SDK to access directory profile
- Easy sign up and sign in
- comes with a customizable web UI
- Can use any SAML 2.0 identity providers
- MFA support
- comes with a credentials check option (have I've been **pwnd**?)
- Comes with account takeover protection
- Phone or email verification
- Can define custom workflows
- Supports user migration
- Can also run [[Lambda]] triggers.

## Identity Pools
- Maps an identity or a group to AWS credentials.
- Provide **AWS** credentials to grant access to AWS **resources**.
- Use user pool to authenticate, then use identify pools for **granular** access rights.
