# run-terraform-test-suite
Github action for running Go tests on AWS Terraform fixtures

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| goVersion | the version of Go used for the provided test suites | `string` | n/a | yes |
| terraformVersion | the version of Terraform used for the provided fixtures | `string` | n/a | yes |
| fixtureDirectories | an array of directories to run the test suites against | `string[]` | n/a | yes |
| testFileDirectories | an array of directories containing the test suites for the provided fixtures | `string[]` | n/a | yes |
| awsAccessKeyId | your AWS Access Key ID for the fixtures | `string` | n/a | yes |
| awsSecretAccessKey | your AWS Secret Access Key for the fixtures | `string` | n/a | yes |

## Secrets

## .env variables

## Usage