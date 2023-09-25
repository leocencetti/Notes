## AWS configuration
Three configuration options:
1. Imperative configuration using a bash script and `AWS CLI`.
2. Declarative configuration using `AWS CloudFormation` (complex).
3. Declarative configuration using `AWS CDK` (template generator for `CloudFormation`).

## Region selection
It's recommended to select the `eu-west-1 (ireland)` server since it's the largest and most updated one in Europe.

## AWS Security

### Identity and Access Management (IAM)
- Users are entities that can have access to some resources. Can be real or tokens
- Each `user` can impersonate a `role`, which provides a time-limited, scoped, access to a specific subset of APIs. The role is a set of `policies` that provide granular control over the permissions.   
## Using the CLI
1. Install the latest AWS CLI (v2) using the [following link](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html#cliv2-linux-install). 
2. Configure the SSO authentication for the shell with `aws configure sso`. Fill in the options:
	- SSO session name: ??
	- SSO start URL: `https://flybotix.awsapps.com/start#`
	- SSO region: `eu-west-1`
	- SSO registration scopes: default
	- Default client region: `eu-west-1`
	- Profile name: `rnd-devops`
1. Authenticate the shell with `aws sso login --profile rnd-devops`.
### Pushing an image to ECR
1. Login into ECR with: `aws ecr get-login-password --region eu-west-1 --profile <profile> | docker login --username AWS --password-stdin 125508840959.dkr.ecr.eu-west-1.amazonaws.com`
2. Ensure that a repository for the image exists. If not, you can create one from the CLI with: `aws ecr create-repository --repository-name <image-name> --image-tag-mutability IMMUTABLE --region eu-west-1 --profile <profile>`
3. Tag image with correct name: `docker tag <image> 125508840959.dkr.ecr.eu-west-1.amazonaws.com/<image-name>:<image-tag>`
4. Push image with: `125508840959.dkr.ecr.eu-west-1.amazonaws.com/<image-name>:<image-tag>`