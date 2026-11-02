# 🗣️ Vocal — Terraform (Explain Out Loud)

> Definitions: [`../../Definitions/05-Terraform-definitions.md`](../../Definitions/05-Terraform-definitions.md)

## Basics
1. 🟢🔥 `[GEN]` What is Infrastructure as Code? Declarative vs imperative.

    Ans: Infrastructure as Code (IaC) is the practice of managing and provisioning computing infrastructure through machine-readable configuration files, rather than through physical hardware configuration or interactive configuration tools.

2. 🟢🔥 `[TCS][INFY]` Terraform vs CloudFormation vs Ansible.

    Ans: Terraform, CloudFormation, and Ansible are all tools for managing infrastructure, but they have different approaches and use cases. Terraform is a declarative IaC tool that supports multiple cloud providers and focuses on provisioning and managing infrastructure. CloudFormation is AWS-specific and also declarative, allowing you to define AWS resources using JSON or YAML templates. Ansible is primarily an imperative configuration management tool that can also provision infrastructure, using playbooks written in YAML to define tasks and configurations.

3. 🟢 `[CTS]` What do `init`, `plan`, `apply`, `destroy` do?

    Ans: `init` initializes a Terraform working directory, setting up backend configuration and downloading provider plugins. `plan` creates an execution plan, showing what actions Terraform will take to achieve the desired state. `apply` executes the plan, making changes to reach the desired state. `destroy` removes all resources managed by the configuration.

4. 🟢 `[HEXA]` Resource vs data source.

    Ans: A resource in Terraform represents a component of your infrastructure that you want to create, update, or delete. A data source, on the other hand, allows you to fetch and use information about existing resources that are not managed by your Terraform configuration.

5. 🟡 `[CAPG]` variable vs local vs output.

    Ans: In Terraform, a variable is used to define input values that can be passed into a module or configuration, allowing for dynamic and reusable configurations. A local is a named value that is computed from other values within the configuration, providing a way to simplify complex expressions and avoid repetition. An output is a value that is exported from a module or configuration, making it accessible to other modules or for display after applying the configuration.

## State 🔥🔥
6. 🟡🔥 `[WMT][PP]` What is the state file? Why does Terraform need it?

    Ans: The state file is a JSON file that Terraform uses to keep track of the resources it manages. It contains information about the current state of the infrastructure, including resource IDs, attributes, and metadata. Terraform needs the state file to determine what changes need to be made when applying a configuration, as it compares the desired state defined in the configuration files with the actual state recorded in the state file.

7. 🟡🔥 `[WMT]` Why a remote backend? How does state locking work? (S3 + DynamoDB)

    Ans: A remote backend in Terraform allows the state file to be stored in a centralized location, such as an S3 bucket, enabling collaboration among multiple team members. State locking, often implemented using DynamoDB, prevents concurrent modifications to the state file by locking it during operations like `apply` or `plan`, ensuring consistency and avoiding conflicts.

8. 🔴 `[AMZN]` Two engineers run `apply` at once — what happens / how prevented?

    Ans: If two engineers run `apply` simultaneously, it can lead to race conditions and inconsistent state. Terraform prevents this by using state locking when a remote backend is configured. The first `apply` operation acquires a lock on the state file, and the second operation will be blocked until the lock is released, ensuring that only one operation modifies the state at a time.

9. 🟡🔥 `[CTS]` How do you bring existing infra under Terraform? (`import`)

    Ans: To bring existing infrastructure under Terraform management, you can use the `terraform import` command. This command allows you to import existing resources into your Terraform state file, associating them with the corresponding resource blocks in your configuration. After importing, you may need to update your configuration files to match the imported resources' attributes and settings.

10. 🔴 `[PP]` What is drift? How do you detect and fix it?

    Ans: Drift occurs when the actual state of the infrastructure diverges from the desired state defined in the Terraform configuration. This can happen due to manual changes made outside of Terraform or changes made by other tools. To detect drift, you can run `terraform plan`, which will show any differences between the current state and the desired state. To fix drift, you can either update the Terraform configuration to match the actual state or use `terraform apply` to bring the infrastructure back in line with the desired state.

11. 🔴 `[WMT]` Can you edit the state file manually? Why is that dangerous?

    Ans: While it is technically possible to edit the Terraform state file manually, it is highly discouraged and considered dangerous. The state file contains critical information about the resources managed by Terraform, and manual edits can lead to inconsistencies, corruption, or loss of data. If the state file is modified incorrectly, it can cause Terraform to misinterpret the current state of the infrastructure, leading to unexpected behavior during future operations. It is recommended to use Terraform commands and features to manage state rather than editing the file directly.


## Modules & structure 🔥
12. 🟡🔥 `[INFY][LTIM]` What is a module? How do you design reusable ones? (your −50% setup line)

    Ans: A module in Terraform is a container for multiple resources that are used together. Modules can be reused across different parts of your configuration or even across different projects. To design reusable modules, you should define clear input variables and output values, encapsulate related resources, and follow a consistent naming convention. This allows you to create modular, maintainable, and scalable infrastructure.

13. 🟡 `[ACN]` count vs for_each — when each?

    
    Ans: In Terraform, `count` and `for_each` are both used to create multiple instances of a resource, but they have different use cases. `count` is used when you want to create a specific number of identical resources, and it is based on an integer value. `for_each`, on the other hand, is used when you want to create resources based on a collection (like a list or map) and allows for more complex configurations, as each instance can have unique attributes based on the collection's elements.

14. 🟡 `[CMCST]` How do you manage multiple environments (dev/stage/prod)?

    Ans: To manage multiple environments in Terraform, you can use workspaces, separate directories for each environment, or a combination of both. Workspaces allow you to maintain different states for the same configuration, while using separate directories enables you to have distinct configurations for each environment. Additionally, you can use variables and backend configurations to customize settings for each environment.

15. 🟡 `[CAPG]` What are workspaces? Workspaces vs directory-per-env.

    Ans: Workspaces in Terraform are a way to manage multiple instances of a configuration, each with its own state file. They allow you to switch between different environments (like dev, stage, prod) without changing the configuration files. In contrast, using a directory-per-env approach involves creating separate directories for each environment, each containing its own configuration files and state. Workspaces are more lightweight and easier to manage for simple use cases, while directory-per-env provides more isolation and flexibility for complex setups.


## Lifecycle & safety
16. 🟡 `[DLT]` `create_before_destroy`, `prevent_destroy`, `ignore_changes` — uses.

    Ans: In Terraform, `create_before_destroy` is used to ensure that a new resource is created before the old one is destroyed, which helps prevent downtime. `prevent_destroy` is a safeguard that prevents a resource from being accidentally destroyed. `ignore_changes` is used to ignore changes to specific attributes of a resource, allowing Terraform to manage other aspects without affecting the ignored attributes.

17. 🟡 `[EY]` How do you force-recreate a resource? (`taint` / `-replace`)

    Ans: To force-recreate a resource in Terraform, you can use the `terraform taint` command to mark a resource as tainted, which will cause it to be destroyed and recreated on the next `apply`. Alternatively, you can use the `-replace` option with the `terraform apply` command to specify that a particular resource should be replaced, leading to its destruction and recreation.

18. 🟡🔥 `[PP]` How do you handle secrets in Terraform?

    Ans: Handling secrets in Terraform can be done using several approaches. One common method is to use environment variables or a secrets manager (like AWS Secrets Manager or HashiCorp Vault) to store sensitive information. You can then reference these secrets in your Terraform configuration without hardcoding them. Additionally, you can use the `sensitive` attribute in output variables to prevent sensitive data from being displayed in the Terraform output.

19. 🟡🔥 `[WMT]` Your Terraform CI/CD flow? (plan on PR, apply on merge)

    Ans: A typical Terraform CI/CD flow involves running `terraform plan` on pull requests (PRs) to preview the changes that will be made to the infrastructure. This allows team members to review and approve the changes before they are applied. Once the PR is merged, `terraform apply` is executed to implement the approved changes in the target environment. This workflow helps ensure that infrastructure changes are reviewed and controlled, reducing the risk of errors or unintended modifications.

20. 🔴 `[AMZN]` How do you scan Terraform for misconfig? (Checkov, tflint)

    Ans: To scan Terraform configurations for misconfigurations, you can use tools like Checkov and TFLint. Checkov is a static analysis tool that scans Terraform code for security and compliance issues, while TFLint focuses on detecting errors and best practices in Terraform configurations. These tools help ensure that your infrastructure code adheres to security and operational standards before deployment.

---
### ⭐ Your resume line
- "Reusable Terraform modules, −50% env setup" → describe module inputs/outputs + remote S3 backend with DynamoDB lock.
