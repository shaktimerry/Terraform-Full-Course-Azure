## Task for Day05

- Using the files created in the previous task (day04), update them to use variables below
- Add an input variable named "environment" and set the default value to "staging"
- Create the terraform.tfvars file and set the environment value to demo
- Test the variable precedence by passing the variables in different ways: tfvars file, environment variables, default, etc.
- Create a local variable with a tag called common_tags with values as env=dev, lob=banking, stage=alpha, and use the local variable in the tags section of main.tf
- Create an output variable to print the storage account name

Note : 

Method 1 : By Writing Variable inside tf file > You write anything in variable section default value.
Precedence can happen during tf plan

Ex : Suppose default value is QA. But during apply you did " tf plan -var=environment=dev "
It changes to Dev.

Method 2 : Create terraform.tfvars file
environment = "demo"

The Three Types of Variables (Input, Output, Locals)
******************************************************************************
Input Variables (variable / IP): The knobs and dials you feed in from the outside. They let you customize your code without rewriting it (e.g., passing in an environment name or instance size). //-var=environment=dev

Output Variables (output / OP): The report card passed out after creation. They display important info on your screen or pass data to other modules (e.g., printing the public IP address of a newly created server so you can use it).

output "storage_account_name" {
  value = azurerm_storage_account.example.name
}

Local Variables (locals): The internal scratchpad. Users don't type these in; Terraform calculates them behind the scenes to keep your code clean and prevent you from repeating yourself (DRY principle). Often doesn't change same key pair value everywhere. // local.common_tags.environment


Data Types (String and All)
*****************************************
Terraform is typed, meaning variables expect specific kinds of data:

String: Plain text wrapped in quotes (e.g., "t2.micro", "us-east-1").

Number: Numeric values without quotes (e.g., 80, 5, 1024).

Bool: True or false flags (e.g., true, false).

List: An ordered sequence of values inside brackets (e.g., ["subnet-1", "subnet-2", "subnet-3"]).

Map: A key-value dictionary (e.g., { Environment = "Prod", Owner = "DevOps" }).

Object / Tuple: Advanced custom structures for bundling mixed data types together.

3. Quick Recap on Variable Precedence
*******************************************************
If you define a variable in multiple places, Terraform resolves conflicts using this order (from lowest priority to highest):

Default values written inside the code.

Environment variables (TF_VAR_variable_name).

terraform.tfvars file.

Auto-load files (*.auto.tfvars).

Command-line flags (-var or -var-file) — This always wins.
