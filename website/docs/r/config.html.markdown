---
layout: "heroku"
page_title: "Heroku: heroku_config"
sidebar_current: "docs-heroku-resource-config"
description: |-
  Provides a Heroku Config resource, making it possible to define variables that can be used in other Heroku terraform resources.
---

# heroku\_config
Provides a Heroku Config resource, making it possible to define variables 
to be used throughout your Heroku terraform configurations. Combined with `heroku_config_association`,
these two resources enable users to decouple setting config var(s) from the `heroku_app` resource.

~> **NOTE:** Unlike most Terraform resources, this resource **DOES NOT** by itself create, update or delete anything on Heroku. 
A [`heroku_config_association`](config_association.html), `heroku_app.config_vars`, or `heroku_app.sensitive_config_vars` is required to actually set these values on Heroku apps.

## Example HCL
```hcl
resource "heroku_config" "endpoints" {
    name = "endpoints"

    vars = {
        x = "https://..."
        y = "https://..."
        z = "https://..."
    }

    sensitive_vars = {
        PRIVATE_KEY="some_private_key"
    }
}
```

## Argument Reference
* `name` - (Required) Name of the var(s). This could be anything to uniquely identify the var(s).
* `vars` - Map of vars that are can be outputted in plaintext
* `sensitive_vars` - This is the same as `vars`. The main difference between the two
attributes is when `sensitive_vars` outputs are displayed on-screen following a terraform
apply or terraform refresh, they are redacted, with <sensitive> displayed in place of their value.
It is recommended to put private keys, passwords, etc in this argument.

## Attributes Reference
The following attributes are exported:
* `id` - The ID of the config

## Import
As this resource does not make any changes remotely to your Heroku account, it is not possible to import existing `heroku_config` configuration(s).
