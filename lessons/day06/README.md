## Task for Day06

### Using the files from previous task(day05), divide the entire folder structure into seperate files such as
- backend.tf
- provider.tf
- resource-group.tf
- storage-account.tf
- local.tf
- variables.tf
- terraform.tfvars
- output.tf



TF executes files in alphabate manner. Like RG first then Storage account
If suppose any resource there which starts with A and it depends with RG.

Then we can do 2 things as Internal Dependecy and External dependency using depends on (but try to use internal dependecy)
