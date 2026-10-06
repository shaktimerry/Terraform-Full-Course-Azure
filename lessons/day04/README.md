# Day04 - Terraform State File

## How Terraform update Infrastructure

- Goal is to keep the actual state same as the desired state
- The actual state resides inside a file called statefile
  
<img width="618" alt="image" src="https://github.com/user-attachments/assets/66582b79-fd7f-41b7-b287-974319bef8d8" />

## State file best practices

<img width="587" alt="image" src="https://github.com/user-attachments/assets/7e0b774f-bf83-4576-b8e8-618ee248f8f7" />

## Assignment for day04

- Create Azure resources such as resource group and storage account using a remote backend


1. The Desired State (The Blueprint)
 *************************************
What it is: Your Terraform code.

The Layman View: This is the architect's blueprint you draw on paper. It says: "I want a house with 3 bedrooms, 2 bathrooms, and a red front door."

In tech terms: You write code describing the servers, databases, and networks you want to exist.

2. The Actual State (Reality)
*************************************
What it is: What is genuinely running in your cloud provider (like AWS, Azure, or Google Cloud) right now.

The Layman View: This is the physical land. Right now, there might only be a concrete foundation and 2 bedrooms built.

The gap: Sometimes things change in the real world outside of Terraform (someone manually deletes a server or modifies a setting).

3. The Statefile (Terraform’s Memory Book)
   *************************************
What it is: A file (usually named terraform.tfstate) that Terraform keeps as a diary or memory log.

The Layman View: This is the clipboard your construction manager carries. It links your blueprint to reality—recording notes like: "Blueprint bedroom #1 is tied to physical Room A in the building, and it currently has a blue coat of paint."

Why it matters: Cloud providers are huge and don't inherently know which server belongs to which piece of code. The statefile is the bridge that connects your code to the actual cloud resources.

How They Work Together
*************************************
When you run Terraform, it goes through a three-step dance:

Checks the Memory (Statefile): It looks at its diary to see what it last built.

Inspects Reality (Actual State): It pings the cloud to see what is actually running right now.

Compares to the Code (Desired State): It looks at your blueprint. If the blueprint asks for 3 servers, but the cloud only has 2, Terraform says: "Aha! We are missing one. Let me build it for you."
