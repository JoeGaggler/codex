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
