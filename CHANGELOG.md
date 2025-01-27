## 1.6.0 (Unreleased)

NEW FEATURES:
* `terraform test`: The previously experimental `terraform test` command has been moved out of experimental. This comes with a significant change in how Terraform tests are written and executed.

    Terraform tests are now written within `.tftest.hcl` files, controlled by a series of `run` blocks. Each `run` block will execute a Terraform plan or apply command against the Terraform configuration under test and can execute conditions against the resultant plan and state.

ENHANCEMENTS:
* cli: Improve schema caching to reduce memory footprint with large providers ([#33486](https://github.com/hashicorp/terraform/pull/33486))
* cloud: Remote plans on Terraform Cloud/Enterprise can now be saved using the `-out` flag, referenced in the `show` command, and applied by specifying the plan file name. ([#33492](https://github.com/hashicorp/terraform/issues/33492))
* config: Terraform can now track some additional detail about values that won't be known until the apply step, such as the range of possible lengths for a collection or whether an unknown value can possibly be null. When this information is available, Terraform can potentially generate known results for some operations on unknown values. This doesn't mean that Terraform can immediately track that detail in all cases, but the type system now contains the facility for that and so over time we will improve the level of detail generated by built-in functions, language operators, Terraform providers, etc. ([#33234](https://github.com/hashicorp/terraform/issues/33234))
* config: The `import` block `id` field now accepts an expression referencing other values such as resource attributes, as long as the value is a string known at plan time. ([#33618](https://github.com/hashicorp/terraform/issues/33618))
* jsonplan: Added `errored` field to JSON plan output, indicating whether a plan errored. ([#33372](https://github.com/hashicorp/terraform/issues/33372))


BUG FIXES:
* The upstream dependency that Terraform uses for service discovery of Terraform-native services such as Terraform Cloud/Enterprise state storage was previously not concurrency-safe, but Terraform was treating it as if it was in situations like when a configuration has multiple `terraform_remote_state` blocks all using the "remote" backend. Terraform is now using a newer version of that library which updates its internal caches in a concurrency-safe way. ([#33364](https://github.com/hashicorp/terraform/issues/33364))
* Transitive dependencies were lost during apply when the referenced resource expanded into zero instances ([#33403](https://github.com/hashicorp/terraform/issues/33403))
* Terraform will no longer override SSH settings in local git configuration when installing modules. ([#33592](https://github.com/hashicorp/terraform/issues/33592))

S3 BACKEND

Update Notes

* Moves arguments associated with assuming an IAM role into nested block `assume_role`.
  This deprecates the arguments `role_arn`, `session_name`, `external_id`, `assume_role_duration_seconds`, `assume_role_policy`, `assume_role_policy_arns`, `assume_role_tags`, and `assume_role_transitive_tag_keys`. [GH-33630]
* Supports the default AWS environment variables for overrding API endpoints: `AWS_ENDPOINT_URL_DYNAMODB`, `AWS_ENDPOINT_URL_IAM`, `AWS_ENDPOINT_URL_S3`, and `AWS_ENDPOINT_URL_STS`.
  This deprecates the environment variables `AWS_DYNAMODB_ENDPOINT`, `AWS_IAM_ENDPOINT`, `AWS_S3_ENDPOINT`, and `AWS_STS_ENDPOINT`. [GH-33715]

## Previous Releases

For information on prior major and minor releases, see their changelogs:

* [v1.5](https://github.com/hashicorp/terraform/blob/v1.5/CHANGELOG.md)
* [v1.4](https://github.com/hashicorp/terraform/blob/v1.4/CHANGELOG.md)
* [v1.3](https://github.com/hashicorp/terraform/blob/v1.3/CHANGELOG.md)
* [v1.2](https://github.com/hashicorp/terraform/blob/v1.2/CHANGELOG.md)
* [v1.1](https://github.com/hashicorp/terraform/blob/v1.1/CHANGELOG.md)
* [v1.0](https://github.com/hashicorp/terraform/blob/v1.0/CHANGELOG.md)
* [v0.15](https://github.com/hashicorp/terraform/blob/v0.15/CHANGELOG.md)
* [v0.14](https://github.com/hashicorp/terraform/blob/v0.14/CHANGELOG.md)
* [v0.13](https://github.com/hashicorp/terraform/blob/v0.13/CHANGELOG.md)
* [v0.12](https://github.com/hashicorp/terraform/blob/v0.12/CHANGELOG.md)
* [v0.11 and earlier](https://github.com/hashicorp/terraform/blob/v0.11/CHANGELOG.md)
