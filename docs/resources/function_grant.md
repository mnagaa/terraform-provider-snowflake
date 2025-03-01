---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "snowflake_function_grant Resource - terraform-provider-snowflake"
subcategory: ""
description: |-
  
---

# snowflake_function_grant (Resource)



## Example Usage

```terraform
resource "snowflake_function_grant" "grant" {
  database_name       = "database"
  schema_name         = "schema"
  function_name       = "function"
  argument_data_types = ["array", "string"]
  privilege           = "USAGE"
  roles               = ["role1", "role2"]
  shares              = ["share1", "share2"]
  on_future           = false
  with_grant_option   = false
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `database_name` (String) The name of the database containing the current or future functions on which to grant privileges.
- `roles` (Set of String) Grants privilege to these roles.

### Optional

- `argument_data_types` (List of String) List of the argument data types for the function (must be present if function has arguments and function_name is present)
- `arguments` (Block List, Deprecated) List of the arguments for the function (must be present if function has arguments and function_name is present) (see [below for nested schema](#nestedblock--arguments))
- `enable_multiple_grants` (Boolean) When this is set to true, multiple grants of the same type can be created. This will cause Terraform to not revoke grants applied to roles and objects outside Terraform.
- `function_name` (String) The name of the function on which to grant privileges immediately (only valid if on_future is false).
- `on_future` (Boolean) When this is set to true and a schema_name is provided, apply this grant on all future functions in the given schema. When this is true and no schema_name is provided apply this grant on all future functions in the given database. The function_name, arguments, return_type, and shares fields must be unset in order to use on_future.
- `privilege` (String) The privilege to grant on the current or future function. Must be one of `USAGE` or `OWNERSHIP`.
- `return_type` (String, Deprecated) The return type of the function (must be present if function_name is present)
- `schema_name` (String) The name of the schema containing the current or future functions on which to grant privileges.
- `shares` (Set of String) Grants privilege to these shares (only valid if on_future is false).
- `with_grant_option` (Boolean) When this is set to true, allows the recipient role to grant the privileges to other roles.

### Read-Only

- `id` (String) The ID of this resource.

<a id="nestedblock--arguments"></a>
### Nested Schema for `arguments`

Required:

- `name` (String) The argument name
- `type` (String) The argument type

## Import

Import is supported using the following syntax:

```shell
# format is database name | schema name | function signature | privilege | true/false for with_grant_option
terraform import snowflake_function_grant.example 'dbName|schemaName|functionName(ARG1TYPE,ARG2TYPE)|USAGE|false'
```
