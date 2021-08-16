



































Resource Manager:

- With Resource Manager you can  automate the process of provisioning your Oracle Cloud Infrastructure resources. 

- Using Terraform, Resource Manager helps you install, configure, and manage resources through the "infrastructure-as-code" model.
- A Terraform configuration codifies your infrastructure in declarative configuration files. 
- Resource Manager allows you to share and manage infrastructure configurations and state files across multiple teams and platforms.
- Resource Manager uses Terraform to help you provision, configure, and manage Oracle Cloud Infrastructure (OCI) resources.

- So basically Resource Manager is a fully managed service that lets you provision infrastructure resources on Oracle Cloud Infrastructure. You can bring your Terraform templates definition and easily create and manage your infrastructure resources. 

- It's going to allow you to use infrastructure as a code to automate a provision process across all OCI resources. 
- Resource Manager also integrates with Identity and Access Management, so you can define granular permissions for Terraform operations. So it currently supports command line interface, SDK, and the UI console.

- So here are some Resource Manager benefits. 
  - Resource Manager unlocks infrastructure automation capabilities so you can standardize your infrastructure and easily replicate your environments. 
  - it gives you a deep integration with OCI Platform and enables developers to leverage the entire OCI API catalog.
  - Resource Manager allows you to share and manage infrastructures, configurations, and state files across multiple teams and platforms, improving collaboration. 
  - while you can install and run Terraform locally and use Terraform modules to do specific tasks, developers would be happy to know that OCI Terraform provider functionality is completely supported by Resource Manager. 
  - Resource Manager itself is a free service, where you are paying only for the underlying infrastructure and resources provisioned by Terraform.
  - Resource Manager integrates with Oracle Cloud Infrastructure Identity and Access Management. So customers can define granular permissions for Terraform operations. 
  - you can define policies to allow only a specific group to execute Jobs using Resource Manager and also define what actions they can take. 

 

- Resource Manager has two main components. 
  - Stack
  - Jobs

- Stacks represent as a set of OCI resources you want to create. These, you have all your Terraform files configuration inside of a zip file. 
- Stacks are attached to a specific region and compartments. However, the resources of a given Stack can be deployed in different regions in compartments.

- Jobs perform the actions that are defined in your configuration. Only one Job at a time can run on a given Stack. 
- When you have to run a Job to provision a different set of resources, it's recommended that you create a separate Stack and use a different configuration.

- When working with Resource Manager, all you have to do is make sure that your provider configuration is adjusted to use Resource Manager. That means you can omit the user OCID, private key, fingerprint, and tenancy OCID from your provider configuration. All the rest of the files will remain exactly the same.
- If you need to pass invalid for a variable declared in a Terraform tfvars file or a variables.tf file.
- Resource Manager workflow:
  ![This image shows the workflow for provisioning infrastructure using Resource Manager.](https://docs.oracle.com/en-us/iaas/Content/Resources/Images/rmWorkflow.png)
- 