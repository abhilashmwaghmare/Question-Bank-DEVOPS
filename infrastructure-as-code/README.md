## **🚀 Beginner-Level Infrastructure as Code (IaC) Questions (1-20)**

#### *(Terraform, Ansible, CloudFormation)*

### **Terraform Questions**  

### **1. What is Infrastructure as Code (IaC) and why is it important?**  

**Answer:**  
Infrastructure as Code (IaC) is a **method of managing and provisioning infrastructure** using code instead of manual processes. It allows:  
✅ **Automation** of infrastructure deployment  
✅ **Consistency** by reducing human errors  
✅ **Scalability** through repeatable scripts  

---

### **2. What is Terraform and how does it work?**  

**Answer:**  
Terraform is an **open-source IaC tool** by HashiCorp that helps define and provision infrastructure using a declarative configuration language. It follows three steps:  

1. **Write**: Define infrastructure in `.tf` files  
2. **Plan**: Preview changes before applying  
3. **Apply**: Deploy and manage resources  

Example:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "my_instance" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

---

### **3. What is the difference between Terraform and Ansible?**  

**Answer:**  

| Feature | Terraform | Ansible |
|---------|----------|---------|
| **Type** | Declarative | Imperative |
| **Purpose** | Infrastructure provisioning | Configuration management |
| **State Management** | Uses state file | Stateless |
| **Example Use** | Creating VMs, Networks | Installing software, configuring OS |

---

### **4. What are Terraform Providers?**  

**Answer:**  
Providers are **plugins** that allow Terraform to manage resources on different platforms (AWS, Azure, GCP, Kubernetes, etc.).  

Example:  

```hcl
provider "aws" {
  region = "us-west-2"
}
```

---

### **5. What is a Terraform State File?**  

**Answer:**  
Terraform maintains infrastructure details in a **state file (`terraform.tfstate`)**, which:  
✅ Tracks existing resources  
✅ Enables incremental changes  
✅ Supports remote storage (e.g., S3, Azure Blob)  

To store state remotely:  

```hcl
backend "s3" {
  bucket = "my-terraform-state"
  key    = "terraform.tfstate"
  region = "us-east-1"
}
```

---

### **6. What is the purpose of `terraform init`?**  

**Answer:**  
It initializes the working directory by:  
✅ Downloading providers  
✅ Setting up backend storage  
✅ Validating configuration  

Command:  

```sh
terraform init
```

---

### **7. How does Terraform manage dependencies between resources?**  

**Answer:**  
Terraform uses **implicit and explicit dependencies**:  

- **Implicit:** Recognized automatically  
- **Explicit:** Defined using `depends_on`  

Example:  

```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}

resource "aws_ebs_volume" "data" {
  size          = 10
  availability_zone = "us-east-1a"
  depends_on    = [aws_instance.web]
}
```

---

### **8. What is the difference between Terraform `apply` and `plan`?**  

**Answer:**  

| Command | Purpose |
|---------|---------|
| `terraform plan` | Shows proposed changes before applying |
| `terraform apply` | Executes changes to create/update resources |

---

### **9. What is a Terraform Module?**  

**Answer:**  
A **module** is a reusable collection of Terraform configurations that helps **organize** code.  

Example of a module (`main.tf`):  

```hcl
module "network" {
  source = "./modules/vpc"
}
```

---

### **10. How do you destroy resources in Terraform?**  

**Answer:**  
Use:  

```sh
terraform destroy
```

This removes all resources defined in the configuration.

---

### **Ansible Questions**  

### **11. What is Ansible and how does it work?**  

**Answer:**  
Ansible is an **open-source configuration management tool** that automates tasks like software installation, updates, and deployments. It works **agentless**, using SSH or WinRM.  

---

### **12. What are Ansible Playbooks?**  

**Answer:**  
A playbook is a **YAML-based automation script** that defines tasks to be executed.  

Example (`playbook.yml`):  

```yaml
- name: Install Nginx
  hosts: web
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

---

### **13. What is an Ansible Inventory file?**  

**Answer:**  
The inventory file **lists managed servers** and their details.  

Example (`inventory.ini`):  

```ini
[web]
server1 ansible_host=192.168.1.10
server2 ansible_host=192.168.1.11
```

---

### **14. What is the difference between Ansible Roles and Playbooks?**  

**Answer:**  

| Feature | Playbook | Role |
|---------|---------|------|
| **Scope** | Task-oriented | Component-oriented |
| **Organization** | Single YAML file | Structured directory |
| **Usage** | Small-scale automation | Large-scale projects |

---

### **15. How do you run an Ansible Playbook?**  

**Answer:**  
Command:  

```sh
ansible-playbook playbook.yml -i inventory.ini
```

---

### **16. What is an Ansible Galaxy?**  

**Answer:**  
Ansible Galaxy is a **repository for pre-built Ansible roles**.  

Example:  

```sh
ansible-galaxy install geerlingguy.nginx
```

---

### **17. How does Ansible handle idempotency?**  

**Answer:**  
Ansible ensures **repeated executions produce the same result** by only applying changes when needed.  

Example:  

```yaml
- name: Ensure Nginx is installed
  apt:
    name: nginx
    state: present
```

If Nginx is already installed, the task is skipped.

---

### **18. What is Ansible Vault?**  

**Answer:**  
Ansible Vault **encrypts sensitive data** like passwords.  

To create an encrypted file:  

```sh
ansible-vault encrypt secrets.yml
```

---

### **CloudFormation Questions**  

### **19. What is AWS CloudFormation?**  

**Answer:**  
AWS CloudFormation is an **IaC service** that provisions AWS infrastructure using YAML/JSON templates.  

Example:  

```yaml
Resources:
  MyBucket:
    Type: "AWS::S3::Bucket"
```

---

### **20. How do you create a CloudFormation stack?**  

**Answer:**  
Command:  

```sh
aws cloudformation create-stack --stack-name my-stack --template-body file://template.yml
```

---

## **🚀 Intermediate-Level Infrastructure as Code (IaC) Questions (21-40)**  

#### *(Terraform, Ansible, CloudFormation)*  

---

### **Terraform Questions**  

### **21. What is the difference between Terraform `local` and `remote` state?**  

**Answer:**  
Terraform state can be stored **locally** (on disk) or **remotely** (in S3, Consul, etc.).  

| Storage | Pros | Cons |
|---------|------|------|
| **Local State** (`terraform.tfstate`) | Fast, simple | Not suitable for teams |
| **Remote State** (S3, etc.) | Shared, secure | Slightly slower |

Example remote state (S3 backend):  

```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}
```

---

### **22. How do you handle secrets in Terraform?**  

**Answer:**  
Avoid hardcoding secrets in `.tf` files:  
✅ Use **environment variables**  
✅ Use **Terraform Vault Provider**  
✅ Store secrets in **AWS Secrets Manager**  

Example using environment variables:  

```sh
export TF_VAR_db_password="mypassword"
```

---

### **23. What is Terraform Locking, and why is it important?**  

**Answer:**  
Terraform uses **state locking** to prevent simultaneous updates by multiple users.  

- **Enabled automatically** for remote state backends (e.g., S3 + DynamoDB).  

Example (DynamoDB locking):  

```hcl
backend "s3" {
  bucket         = "my-terraform-bucket"
  dynamodb_table = "terraform-lock"
}
```

---

### **24. What is Terraform Workspaces?**  

**Answer:**  
Terraform **Workspaces** allow managing multiple environments within a single configuration.  

```sh
terraform workspace new dev
terraform workspace select dev
```

---

### **25. How do you create reusable Terraform modules?**  

**Answer:**  
Modules help organize and reuse code.  

Example (`modules/network/main.tf`):  

```hcl
variable "vpc_cidr" {}

resource "aws_vpc" "main" {
  cidr_block = var.vpc_cidr
}
```

Usage:  

```hcl
module "vpc" {
  source   = "./modules/network"
  vpc_cidr = "10.0.0.0/16"
}
```

---

### **26. What is Terraform Cloud and Terraform Enterprise?**  

**Answer:**  

| Feature | Terraform Cloud | Terraform Enterprise |
|---------|----------------|----------------------|
| **Type** | SaaS | Self-hosted |
| **Use Case** | Collaboration, remote state | Large enterprises |
| **Extras** | Remote execution, VCS integration | Advanced security & governance |

---

### **27. How does Terraform handle drift detection?**  

**Answer:**  
Terraform detects drift by running:  

```sh
terraform plan
```

Drift occurs when **actual infrastructure** changes outside Terraform’s control.

---

### **28. How do you use `count` and `for_each` in Terraform?**  

**Answer:**  

- `count` is used for **simple lists**.  
- `for_each` is used for **maps or sets**.  

Example (`count`):  

```hcl
resource "aws_instance" "web" {
  count = 3
  ami   = "ami-12345678"
}
```

Example (`for_each`):  

```hcl
resource "aws_s3_bucket" "buckets" {
  for_each = toset(["dev", "prod"])
  bucket   = "my-app-${each.value}"
}
```

---

### **Ansible Questions**  

### **29. How do you use Ansible variables?**  

**Answer:**  
Variables can be defined in:  
✅ Playbooks (`vars:`)  
✅ Inventory (`host_vars`, `group_vars`)  
✅ Command-line (`-e` flag)  

Example:  

```yaml
- hosts: web
  vars:
    app_port: 8080
  tasks:
    - debug: msg="App runs on port {{ app_port }}"
```

---

### **30. What are Ansible Facts?**  

**Answer:**  
Facts are **system information** collected automatically.  

Example:  

```sh
ansible all -m setup
```

---

### **31. What is the purpose of Ansible Handlers?**  

**Answer:**  
Handlers run **only when notified**.  

Example:  

```yaml
- name: Install Nginx
  apt:
    name: nginx
  notify: Restart Nginx

- name: Restart Nginx
  service:
    name: nginx
    state: restarted
  listen: Restart Nginx
```

---

### **32. How does Ansible manage dependencies?**  

**Answer:**  
Ansible Roles handle dependencies using `meta/main.yml`.  

Example:  

```yaml
dependencies:
  - role: common
```

---

### **33. What is the difference between `command` and `shell` modules in Ansible?**  

**Answer:**  

| Module | When to Use | Example |
|--------|------------|---------|
| `command` | Runs a command without shell features | `ansible all -m command -a "ls"` |
| `shell` | Runs commands with shell features (`|`,`&&`) | `ansible all -m shell -a "echo hello | tee file.txt"` |

---

### **34. What is Ansible Dynamic Inventory?**  

**Answer:**  
Dynamic Inventory **fetches live host lists** from AWS, Azure, GCP.  

Example for AWS:  

```sh
ansible-inventory --list -i aws_ec2.yml
```

---

## **CloudFormation Questions**

### **35. What are the main components of AWS CloudFormation?**  

**Answer:**  

| Component | Description |
|-----------|------------|
| **Templates** | Defines resources in YAML/JSON |
| **Stacks** | Collection of AWS resources |
| **StackSets** | Deploy stacks across multiple accounts |

---

### **36. How do you update a CloudFormation stack?**  

**Answer:**  
Use:  

```sh
aws cloudformation update-stack --stack-name my-stack --template-body file://template.yml
```

---

### **37. What is the difference between `DependsOn` and `CreationPolicy` in CloudFormation?**  

**Answer:**  

| Feature | Purpose |
|---------|---------|
| `DependsOn` | Ensures a resource is created before another |
| `CreationPolicy` | Waits for a signal before marking as successful |

Example (`DependsOn`):  

```yaml
Resources:
  WebServer:
    Type: AWS::EC2::Instance
    DependsOn: MyDB
```

---

### **38. How do you use Conditions in CloudFormation?**  

**Answer:**  
Conditions allow resources to be created based on parameters.  

Example:  

```yaml
Conditions:
  IsProd: !Equals [!Ref EnvType, "Prod"]
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Condition: IsProd
```

---

### **39. What is AWS CloudFormation Drift Detection?**  

**Answer:**  
Detects **manual changes** to resources outside CloudFormation.  

Run drift check:  

```sh
aws cloudformation detect-stack-drift --stack-name my-stack
```

---

### **40. What are Intrinsic Functions in CloudFormation?**  

**Answer:**  
Intrinsic functions **dynamically reference values**.  

Example (`!Sub` for string interpolation):  

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub "${AWS::AccountId}-my-bucket"
```

---

## **🚀 Advanced-Level Infrastructure as Code (IaC) Questions (41-60)**  

#### *(Terraform, Ansible, CloudFormation)*  

---

### **Terraform Questions**  

### **41. How do you implement CI/CD pipelines with Terraform?**  

**Answer:**  
Terraform can be integrated into CI/CD pipelines using **GitHub Actions, GitLab CI, or Jenkins**.  
✅ **Linting & Validation:** `terraform fmt`, `terraform validate`  
✅ **Planning:** `terraform plan -out=tfplan`  
✅ **Apply Changes:** `terraform apply tfplan`  

Example GitHub Actions workflow:  

```yaml
jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v1
      - name: Terraform Init
        run: terraform init
      - name: Terraform Plan
        run: terraform plan -out=tfplan
      - name: Terraform Apply
        run: terraform apply tfplan
```

---

### **42. What are Terraform Data Sources?**  

**Answer:**  
Data sources allow Terraform to **query external resources** without managing them.  

Example:  

```hcl
data "aws_vpc" "existing_vpc" {
  filter {
    name   = "tag:Name"
    values = ["my-vpc"]
  }
}
```

---

### **43. How do you manage Terraform module versions?**  

**Answer:**  
Use version constraints in `source`.  

Example (`versions.tf`):  

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "3.5.0"
}
```

---

### **44. How does Terraform handle circular dependencies?**  

**Answer:**  
Terraform detects and prevents **circular dependencies** by analyzing the **DAG (Directed Acyclic Graph)**.  
Solution:  
✅ **Use `depends_on`** explicitly  
✅ **Refactor resources**  

Example:  

```hcl
resource "aws_instance" "web" {
  depends_on = [aws_s3_bucket.logs]
}
```

---

### **45. What are Terraform `locals` and `output` variables?**  

**Answer:**  

- `locals`: Store **temporary values**  
- `output`: Expose values after deployment  

Example:  

```hcl
locals {
  env_name = "dev"
}

output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

---

### **46. What is a Terraform Sentinel Policy?**  

**Answer:**  
Sentinel is a **policy-as-code framework** that enforces compliance.  

Example policy (`enforce_cost.sentinel`):  

```hcl
import "tfplan"

main = rule { tfplan.cost_estimate.total_monthly_cost < 500 }
```

---

### **47. How do you roll back changes in Terraform?**  

**Answer:**  

- **Option 1:** Use version control (`git revert`)  
- **Option 2:** Manually restore the previous state  
- **Option 3:** Import last known working state:  

  ```sh
  terraform apply "tfstate-previous.json"
  ```

---

### **48. What is Terraform Refresh?**  

**Answer:**  
`terraform refresh` updates the state file **without modifying resources**.  

```sh
terraform refresh
```

---

### **49. How do you enforce security best practices in Terraform?**  

**Answer:**  
✅ Use **IAM least privilege** for Terraform executions  
✅ Store **state files securely** (S3 + DynamoDB)  
✅ Run **security scans** with tools like **tfsec**  

Example:  

```sh
tfsec .
```

---

### **50. How does Terraform manage multi-cloud environments?**  

**Answer:**  
By using **multiple providers** in a single configuration.  

Example (AWS + Azure):  

```hcl
provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  features {}
}
```

---

### **Ansible Questions**  

### **51. How do you test Ansible Playbooks before applying them?**  

**Answer:**  
✅ Use `ansible-lint` for syntax validation  
✅ Use **Molecule** for testing  

Example:  

```sh
molecule test
```

---

### **52. How do you handle error handling in Ansible?**  

**Answer:**  
Use `ignore_errors: yes` or `rescue` blocks.  

Example:  

```yaml
tasks:
  - name: Try to restart service
    service:
      name: nginx
      state: restarted
    ignore_errors: yes
```

---

### **53. How do you implement Ansible Vault in CI/CD?**  

**Answer:**  
Use environment variables to decrypt secrets.  

Example:  

```sh
ANSIBLE_VAULT_PASSWORD="myvaultpassword" ansible-playbook deploy.yml
```

---

### **54. How does Ansible integrate with Kubernetes?**  

**Answer:**  
✅ Use the **k8s module**  
✅ Define Kubernetes manifests in YAML  

Example:  

```yaml
- name: Deploy to Kubernetes
  k8s:
    state: present
    definition: "{{ lookup('file', 'deployment.yml') }}"
```

---

### **55. How do you ensure Ansible Playbooks are idempotent?**  

**Answer:**  
✅ Always use `state: present`  
✅ Run playbooks multiple times to check consistency  

Example:  

```yaml
- name: Ensure Nginx is installed
  apt:
    name: nginx
    state: present
```

---

### **CloudFormation Questions**  

### **56. How do you modularize CloudFormation templates?**  

**Answer:**  
✅ Use **Nested Stacks**  
✅ Use `AWS::CloudFormation::Stack`  

Example:  

```yaml
Resources:
  MyNetworkStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: "https://s3.amazonaws.com/my-bucket/network.yml"
```

---

### **57. How do you manage parameter changes in CloudFormation?**  

**Answer:**  
Use the `--parameters` flag during updates.  

Example:  

```sh
aws cloudformation update-stack --stack-name my-stack \
  --parameters ParameterKey=InstanceType,ParameterValue=t2.large
```

---

### **58. How do you handle stateful resources in CloudFormation?**  

**Answer:**  
✅ Use **Stack Policies** to prevent deletions  
✅ Enable **RetainPolicy** for S3, RDS  

Example:  

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    DeletionPolicy: Retain
```

---

### **59. What is AWS CloudFormation Stack Policy?**  

**Answer:**  
A Stack Policy **prevents accidental updates or deletions**.  

Example:  

```json
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "Update:Delete",
      "Principal": "*",
      "Resource": "*"
    }
  ]
}
```

---

### **60. How do you debug CloudFormation failures?**  

**Answer:**  
✅ Check the **CloudFormation console**  
✅ Use `aws cloudformation describe-stack-events`  
✅ Enable **rollback debugging**  

Example:  

```sh
aws cloudformation describe-stack-events --stack-name my-stack
```

---

## **📢 Contribute & Stay Updated**  

💡 **Want to contribute?**  
We **welcome contributions!** If you have insights, new tools, or improvements, feel free to submit a **pull request**.  

📌 **How to Contribute?**

- Read the **[CONTRIBUTING.md](https://github.com/abhilash/DevOps-Interview-Questions/blob/master/CONTRIBUTING.md)** guide.  
- Fix errors, add missing topics, or suggest improvements.  
- Submit a **pull request** with your updates.  

📢 **Stay Updated:**  
⭐ **Star the repository** to get notified about new updates and additions.  
💬 **Join discussions** in **[GitHub Issues](https://github.com/abhilash/DevOps-Interview-Questions/issues)** to suggest improvements.  

---

## **🌍 Community & Support**  

🔗 **GitHub:** [@abhilash](https://github.com/abhilash)  
📝 **Blog:** [ProDevOpsGuy](https://blog.prodevopsguy.xyz)  
💬 **Telegram Community:** [Join Here](https://t.me/prodevopsguy)  

![Follow Me](https://imgur.com/2j7GSPs.png)
