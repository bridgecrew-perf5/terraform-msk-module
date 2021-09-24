## Terraform AWS MSK Cluster

Terraform code to create [Msk Kafka Cluster](https://aws.amazon.com/msk/) resource on AWS.

## Requirements

| Name      | Version |
| --------- | ------- |
| terraform | >= 0.13 |

## Providers

| Name | Version |
| ---- | ------- |
| aws  | n/a     |

## Usage

```hcl
provider "aws" {
  region = "us-east-1"
}

module "msk" {
  source = "github.com/antonio-rufo/terraform-msk-module"

  vpc_id                 = "vpc-df4cXXXX"
  msk_subnet_ids         = ["subnet-e129XXXX", "subnet-6c33XXXX"]
  msk_security_group_ids = ["sg-652fXXXX"]
  region                 = "us-east-1"
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| additional_tags | A mapping of additional tags to assign to all resources. | `map(string)` | `{}` | no |
| app_name | Application name abbreviation. Cannot be more than 5 characters long and no less than 2 and must also be lower case. | `string` | `"app"` | no |
| costcenter | Costcenter associated with these resoures. | `string` | `cc` | no |
| cloudwatch\_logs\_group\_name | Name of the Cloudwatch Log Group to deliver logs to. | `string` | `""` | no |
| encryption\_at\_rest\_kms\_key\_arn | You may specify a KMS key short ID or ARN (it will always output an ARN) to use for encrypting your data at rest. If no key is specified, an AWS managed KMS ('aws/msk' managed service) key will be used for encrypting the data at rest. | `string` | `""` | no |
| encryption\_in\_transit\_client\_broker | Encryption setting for data in transit between clients and brokers. Valid values: TLS, TLS\_PLAINTEXT, and PLAINTEXT. Default value is TLS\_PLAINTEXT. | `string` | `"TLS"` | no |
| encryption\_in\_transit\_in\_cluster | Whether data communication among broker nodes is encrypted. Default value: true. | `bool` | `true` | no |
| enhanced\_monitoring | Specify the desired enhanced MSK CloudWatch monitoring level to one of three monitoring levels: DEFAULT, PER\_BROKER, PER\_TOPIC\_PER\_BROKER or PER\_TOPIC\_PER\_PARTITION. See [Monitoring Amazon MSK with Amazon CloudWatch](https://docs.aws.amazon.com/msk/latest/developerguide/monitoring.html). | `string` | `"PER_BROKER"` | no |
| environment | Environment the resources are being provisioned for. Valid options are 'prod', 'uat', 'dev', 'qa' 'sandbox'. | `string` | `"dev"` | no |
| msk_subnet_ids | List of subnet IDs to use for MSK private subnets. | `list(string)` | `["subnet-XXXXXXXX", "subnet-XXXXXXXX"]` | no |
| msk_security_group_ids | A list of security group IDs to assign to the MSK cluster. | `list(string)` | `["sg-XXXXXXXX"]` | no |
| region | Region where resources will be created. | `string` | `"us-east-1"` | no |
| owner | Resource owners Active Directory user id. | `string` | `"owner"` | no |
| vpc_id | ID of the VPC in which MSK will be attached. | `string` | `vpc-XXXXXXXX` | no |

## Outputs

| Name | Description |
|------|-------------|
| bootstrap\_brokers\_tls | TLS connection host:port pairs. |
| zookeeper\_connect\_string | A comma separated list of one or more hostname:port pairs to use to connect to the Apache Zookeeper cluster. |
