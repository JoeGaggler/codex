module: a folder with `.tf` files

include submodule:
```hcl
module "sub_mod_name" {
  source = "subfolder"

  for_each = ...

  some_string = each.key
  some_array  = []
}
```

`some_string` becomes a `variable` in the scope of the module

backend
```hcl
terraform {
  backend "azurerm" { }
}
```

provider
```hcl
provider "azurerm" {
  features { }
}
```

# snippets
## for_each cross join

cross "replicas" with "settings"
```hcl
for_each = {
  for i in flatten([
    for replica_key, replica_value in module.vars.env.replicas : [
      for setting_key, setting_value in {
        "alpha" = replica_value.alpha
        "beta"  = replica_value.beta
      } :
      {
        label = "${replica_key}_${setting_key}"
        key   = setting_key
        value = setting_value
      }
    ]
  ]) : i.label => i
}
```

result:
```json
{
	"replica1_alpha" : {
		"key" : "alpha",
		"value" : "somevaluehere"
	},
	"replica1_beta" : {
		"key" : "beta",
		"value" : "somevaluehere"
	},
	"replica2_alpha" : {
		"key" : "alpha",
		"value" : "somevaluehere"
	},
	"replica2_beta" : {
		"key" : "beta",
		"value" : "somevaluehere"
	}
}
```
