# AWS Verified Access implementation

Built on AWS Zero Trust guiding principles, AWS Verified Access validates each and every application request before granting access. Verified Access removes the need for a VPN, which simplifies the remote connectivity experience for end users and reduces the management complexity for IT administrators. "[AWS Official documentation](https://aws.amazon.com/verified-access/ "AWS Official documentation")"

## Cloudformation stack

In the following lab, we will deploy a basic network, and deploy an example private corporate app running on ECS inside a private segment, we will use AWS verified access service to access the corporate app through our AWS SSO identity provider, this way we don't need the VPN implementation to access to our private network.

## Prerequisites:

- Route 53 public hosted zone.
- Public ACM certificate.
- IAM Identity Center (SSO)

![AWS Verified Access](./Diagram.png)

## Deploying our Cloudformation stack

- Option 1 using AWS CLI:

```javascript
aws cloudformation deploy \
--stack-name aws-verified-access-stack \
--template-file DeploymentStack.yaml \
--parameter-overrides VpcCidrBlock=<your_cidr_block> HostedZone=<your_public_hosted_zone> DomainAcmCertificateArn=<your_acm_certificate_arn> \
--capabilities CAPABILITY_NAMED_IAM \
--profile <your_aws_local_profile>
```

- Option 2 using SAM CLI:

```javascript
sam deploy --stack-name aws-verified-access-stack \
--template-file DeploymentStack.yaml \
--capabilities CAPABILITY_NAMED_IAM \
--resolve-s3 \
--parameter-overrides VpcCidrBlock=<your_cidr_block> HostedZone=<your_public_hosted_zone> DomainAcmCertificateArn=<your_acm_certificate_arn> \
--profile <your_aws_local_profile>
```
