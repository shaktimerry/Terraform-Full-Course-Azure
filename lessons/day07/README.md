## Task for Day07

### Using the files from previous task(day06) , understand the use the below type constraints

- Name: environment, type=string
- Name: storage-disk, type=number
- Name: is_delete, type=boolean
- Name: Allowed_locations, type=list(string)
- Name: resource_tags , type=map(string)
- Name: network_config , type=tuple([string, string, number])
- Name: allowed_vm_sizes, type=list(string)
- Name: vm_config,
```
  type = object({
    size         = string
    publisher    = string
    offer        = string
    sku          = string
    version      = string
  })
```

1. Primitive Types (The Basics)
************************************
string: Plain text wrapped in quotes.

number: Numeric values (integers or decimals) without quotes.

bool: True or false values.

variable "server_name" {
  type    = string
  default = "web-server"
}

variable "max_instances" {
  type    = number
  default = 5
}

variable "enable_monitoring" {
  type    = bool
  default = true
}

2. Collection and Structural Types (Grouped Data)
***********************************************************
list(...): An ordered list of items of the same type.

map(...): A dictionary of key-value pairs.

object({...}: A custom bundle with mixed types.

variable "availability_zones" {
  type    = list(string)
  default = ["us-east-1a", "us-east-1b", "us-east-1c"]
}

variable "tags" {
  type = map(string)
  default = {
    Environment = "staging"
    Project     = "Alpha"
  }
}

List vs. Tuple: What's the Difference?
A list(...) is like a box of identical items: Every single item inside must be the exact same type. If you declare type = list(string), every item must be text.

A tuple([...]) is like a pill organizer with mixed contents: Each slot in the tuple has its own dedicated data type rule.

variable "server_profile" {
  type    = tuple([string, number, bool])
  default = ["web-prod", 443, true]
}

Constraints (Keeping Bad Data Out)
*************************************
Constraints stop someone from breaking your deployment by typing the wrong thing. There are two levels of constraints in Terraform:

1. Basic Constraint: The Type Itself (type = ...)
Just declaring type = number is a constraint. If a user tries to pass a text string like "five" instead of the number 5, Terraform immediately throws an error and stops.

2. Advanced Constraint: Custom Validation Rules (validation)
Sometimes a basic type isn't enough. You might want to allow a string, but only if it matches specific rules (e.g., environment can only be dev, staging, or prod).

Terraform lets you write a validation block inside your variable to enforce this:

Example:

Terraform
variable "environment" {
  type        = string
  description = "The deployment environment"
  default     = "staging"

  # This is the custom constraint rule!
  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Invalid environment! Choose either dev, staging, or prod."
  }
}
