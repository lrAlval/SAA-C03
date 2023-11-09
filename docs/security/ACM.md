# AWS Certificate Manager

- used for SSL TLS certificate managements provision and deploy
- provide in-flight encryption
- public and private certs
- automatic renewal
- cannot be used on ec2
- will take a few hours to be verified
- can be imported but no automatic renewal
- certificates for CloudFront must be in us-east-1
- for **API** gateway region needs to be created in same region

## Integrations
- [[ELB]]
- [[AWS CloudFront]]
- [[APIGateway]]

## Options
- FQDN
- Wildcard

### Validation Method
- DNS
- Email

## Exp Check
- Daily Expiration Events to Event Bride
- [[AWSConfig]] acm-certifacte-expiration-check
