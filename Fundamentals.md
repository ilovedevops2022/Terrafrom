### What is Infrastructure as Code?
The Problem with Manual Configuration

Manually Configuring your cloud infrastructure allows you to easily start using new service offerings to quickly prototype architectures however it comes with mant downsides:

Its easy to misconfigure a service through human error
Its hard to manage the expected state of configuration for compliance
Its hard to transfer configuration knowledge to other team members
Infrastructure as Code (IaC)

You write a configuration script to automate creating, updating, or destroying cloud infrastructure.

IaC is a blueprint of your infrastructure
IaC allows you to easily share, version, or inventory your cloud infrastructure.
Reference
Infrastructure as Code: What Is It? Why Is It Important?

### Popular Infrastructure as Code tools (IaC)
Declarative

You say what you want, and the rest is filled in. Explicit
More verbose, but zero chance of misconfiguration
Uses scripting languages eg. JSON, YAML, XML
ARM Templates

Supports Azure Only
Azure Blueprints

Supports only Azure
CloudFormation

Only for AWS
Cloud Deployment Manager

Supports on Google Cloud
Terraform

Supports many cloud service providers (CSPs) and cloud services
Imperative

What you see is what you get. Implicit
Less verbose, you cloud end up with misconfiguration
Does more than Declarative
Uses programming languages eg. Python, Ruby, JavaScript


Declarative+
Terraform is declarative but the Terraform Language features imperative-like functionality.

### Declarative

YAML, JSON, XML

Limited or no support for imperative-like features.
In some cases, you can add behaviour by extending the base language. E.g. CloudFormation Macros.
Declarative|Imperative

HCL-ish (Terraform Language)

Supports:

Loops (For Each)
Dynamic Blocks
Locals
Complex Data Structure
Maps, Collections
Imperative

Ruby, Python, JavaScript...


### Infrastructure Lifecycle
What is Infrastructure Lifecycle?

the idea of having clearly defined and distinct work phases which are used by DevOps Engineers to plan, design, build, test, and deliver, maintain and retire cloud infrastructure.

What is Day 0, Day 1, and Day 2?

Day 0-2 is a simplified way to describe phases of an infrastructure lifecycle

Day 0 - Plan and Design
Day 1 - Develop and Iterate
Day 2 - Go live and maintain
Days do not literally mean a 24 hour day and is just a broadway of defining where infrastructure project would be

Reference
Day 0/Day 1/Day 2 - the software lifecycle in the cloud age
Imperative features are the utility of the entire feature set of the programming language.
https://codilime.com/blog/day-0-day-1-day-2-the-software-lifecycle-in-the-cloud-age/

### Infrastructure Lifecycle
How does IaC enhance the Infrastructure Lifecycle?

Reliability

IaC makes changes idempotent, consistent, repeatable, and predictable.

Idempotent

No matter how many times you run IaC, you will always end up with the same state that is expected

Manageability

enable mutation via code
revised, with minimal changes
Sensibility

avoid financial and reputational losses to even loss of life when considering government and military dependencies on infrastructure

Reference
Infrastructure as Code in a Private or Public Cloud
https://www.hashicorp.com/blog/infrastructure-as-code-in-a-private-or-public-cloud

###Non-Idempotent vs Idempotent ​
Non-Idempotent​

When I deploy my IaC config file it will provision and launch 2 virtual machines​

When I update my IaC and deploy again, I will end up with 2 new VMs with a total of 4 VMs​

IaC: 2 VMs​

We expect a state of 2​

We end up with 4

Idempotent​

When I deploy my IaC config file it will provision and launch 2 virtual machines​

When I update my IaC and deploy again, it will update the VMs if changed by modifying or deleting and creating new VMs​

IaC: 2 VMs​

We expect a state of 2​

We end up with 2​

Reference
Infrastructure as Code: Principles, Patterns, and Practices
https://shahadarsh.com/2020/07/12/principles-patterns-and-practices-for-effective-infrastructure-as-code/


###Provisioning vs Deployment vs Orchestration​
​Provisioning​

To prepare a server with systems, data, and software, and make it ready for network operation.​

Using Configuration Management tools like Puppet, Ansible, Chef, Bash scripts, PowerShell, or Cloud-Init you can provision a server.​

​When you launch a cloud service and configure it you are “provisioning”​​

​Deployment​​

Deployment is the act of delivering a version of your application to run a provisioned server.​

Deployment could be performed via AWS CodePipline, Harness, Jenkins, Github Actions, CircleCI​

​Orchestration​​

Orchestration is the act of coordinating multiple systems or services.​

Orchestration is a common term when working with microservices, Containers, and Kubernetes.​

Orchestration could be Kubernetes, Salt, Fabric​

Reference
What's Deployment versus Provisioning versus Orchestration?
https://codefol.io/posts/deployment-versus-provisioning-versus-orchestration/

Self-service provisioning for cloud computing services
https://en.wikipedia.org/wiki/Provisioning_(telecommunications)#Self-service_provisioning_for_cloud_computing_services


###Configuration Drift​
Configuration Drift is when provisioned infrastructure has an unexpected configuration change due to:​

team members manually adjusting configuration options​
malicious actors​
side effects from APIs, SDK, or CLIs.​
eg. a junior developer turns on Delete on Termination for the production database.​

Configuration Drift going unnoticed could be a loss or breach of cloud services and residing data or result in interruption of services or unexpected downtime.​

How to detect configuration drift?​

A compliance tool that can detect misconfiguration eg. AWS Config, Azure Policies, *GCP Security Health Analytics​
Built-in support for drift detection eg. AWS CloudFormation Drift Detection​
Storing the expected state eg. Terraform state files​
How to correct configuration drift?​

A compliance tool that can remediate (correct) misconfiguration e.g. AWS Config​
Terraform refresh and plan commands​
Manually correcting the configuration (not recommended)​
Tearing down and setting up the infrastructure again​
Note: Terraform refresh command is not recommended

Please use the alias command: terraform apply -refresh-only -auto-approve or terraform apply -refresh-only

https://www.terraform.io/cli/commands/refresh#usage

How to prevent configuration drift?​

Immutable infrastructure, always create and destroy, never reuse, Blue, Green deployment strategy.​
Servers are never modified after they are deployed​
Baking AMI images or containers via AWS Image Builder or HashiCorp Packer, or a build server eg. GCP Cloud Run​
Using GitOps to version control our IaC, and peer review every single via Pull Requests change to infrastructure​

Reference

Detecting and Managing Drift with Terraform
https://www.hashicorp.com/blog/detecting-and-managing-drift-with-terraform

Mutable vs Immutable Infrastructure​
​Mutable Infrastructure​

Develop​ → Deploy → Configure

A Virtual Machine (VM) is deployed and then a Configuration Management tool like Ansible, Puppet, Chef, Salt, or Cloud-Init is used to configure the state of the server​

​cloud-init​

​Immutable Infrastructure​​

Develop​ → Configure → Deploy

When a VM is launched and provisioned, it is turned into a virtual image and stored in an image repository. That image is used to deploy VM instances.

​Packer​

 ###What is GitOps?​
GitOps is when you take Infrastructure as Code (IaC) and you use a git repository to introduce a formal process to review and accept changes to infrastructure code, once that code is accepted, it automatically triggers a deploy​

Reference

What is GitOps?
https://about.gitlab.com/topics/gitops/

Automate Terraform with GitHub Actions
https://learn.hashicorp.com/tutorials/terraform/github-actions

###Immutable Infrastructure Guarantee​
Terraform encourages you towards an Immutable Infrastructure architect so you get the following guarantees.​

Cloud Resource Failure – What if an EC2 instance fails a status check?​

Application Failure – What if your post-installation script fails due to a change in a package?​

Time to Deploy - What if I need to deploy in a hurry?​

Worst Case Scenario​

Accidental Deletion​
Compromised by a malicious actor​
Need to Change Regions (region outage)​
No Guarantee of 1-to-1​

Every time Cloud-Init runs post-deploy there is no guarantee it's one-to-one with your other VMs.​

Golden Images​

Guarantee of 1-to-1 with your fleet​
Increased assurance of consistency, security​
Speeds up your deployments​


###HashiCorp​
HashiCorp is a company specializing in managed open-source tools used to support the development and deployment of large-scale service-oriented software installations​

What is HashiCorp Cloud Platform (HCP)?​

HCP is a unified platform to access Hashicorp's various products.​

HCP services are cloud-agnostic ​

support for the main cloud service providers (CSPs)​
eg. AWS, GCP, and Azure​
highly suited for multi-cloud workloads​
HashiCorp Products​
Boundary​

secure remote access to systems based on trusted identity.​

Consul​

service discovery platform. provides a full-featured service mesh for secure service segmentation across any cloud or runtime environment, and distributed key-value storage for application configuration​

Nomad​

scheduling and deployment of tasks across worker nodes in a cluster​

Packer​

tool for building virtual machine images for later deployment.​

Terraform​

infrastructure as code software which enables provisioning and adapting virtual infrastructure across all major cloud provider​

Terraform Cloud – a place to store and manage IaC in the cloud or with teams​

Vagrant​

building and maintenance of reproducible software-development environments via virtualization technology​

Vault​

secrets management, identity-based access, encrypting application data, and auditing of secrets for applications, systems, and users​

###What is Terraform?​
Terraform is an open-source and cloud-agnostic Infrastructure as Code (IaC) tool.​

Terraform uses declarative configuration files. ​

The configuration files are written in HashiCorp Configuration Language (HCL).​

Notable features of Terraform:​

Installable modules​
Plan and predict changes​
Dependency graphing​
State management​
Provision infrastructure in familiar languages​
via AWS CDK​
Terraform Registry with 1000+ providers​
Reference
Infrastructure as Code


###What is Terraform Cloud?​
Terraform Cloud is a Software as Service (SaaS) offering for:​

Remote state storage​
Version Control integrations​
Flexible workflows​
Collaborate on Infrastructure changes​
in a single unified web portal.​ → www.terraform.io/cloud

​Terraform Cloud has a generous free-tier that allows for ​team collaboration for the first 5 users of your organization​

In majority of cases you should be using Terraform Cloud.​

​The only case where you may not want to use it to manage your state file is your company has many regulatory requirements along with a long procurement process so you could use Standard remote backend, Atlantis, or investigate Terraform Enterprise​​

The underlying software for Terraform Cloud and Terraform Enterprise is known as the “Terraform Platform”​

Going Through The Motions​
Terraform can be confusing if we don’t get some practical working knowledge ​

We are going to step through all the actions it takes to launch a Virtual Machine on AWS.​

install terraform​
populate configuration file (main.tf)​
terraform init — download and install the providers in the configuration file​
terraform fmt — formats the configuration file syntax to be consistent with expected standard​
terraform validate — validates the configuration logic against what is expected by providers​
terraform apply — generate an execution plan, have the user review and accept or reject to apply changes​
terraform show — view the current state of remote objects​
terraform state list — list all the remote objects (cloud resources) currently being managed​
create input variables (variables.tf)​
create output values (outputs.tf)​
update configuration file (main.tf)​
terraform apply — to apply updated changes ​
terraform show – to observe updated changes​
terraform output — observe output values​
terraform destroy — to destroy all remote objects​
terraform login — store remote state​
update configure file ()​
Reference
Infrastructure as Code
https://www.terraform.io/intro#infrastructure-as-code


###Terraform Lifecycle​
Code - Write or Update your Terraform configuration file​

init​ - Initialize your project​. Pull latest providers and modules​

plan​ - Speculate what will change​ or Generate a saved execution plan​

validate​ - Ensure types and values are valid​. Ensures required attributes are present​

apply​ - Execute the terraform plan provisioning the infrastructure​

destroy​ - Destroy the remote infrastructure​

Reference
The Benefits of Using Terraform as a Tool for Infrastructure-as-Code (IaC)


Waypoint​

modern workflow to build, deploy, and release across platforms​

 ###Terraform Lifecycle​
Code - Write or Update your Terraform configuration file​

init​ - Initialize your project​. Pull latest providers and modules​

plan​ - Speculate what will change​ or Generate a saved execution plan​

validate​ - Ensure types and values are valid​. Ensures required attributes are present​

apply​ - Execute the terraform plan provisioning the infrastructure​

destroy​ - Destroy the remote infrastructure​

Reference
The Benefits of Using Terraform as a Tool for Infrastructure-as-Code (IaC)
https://www.opensourceforu.com/2020/07/the-benefits-of-using-terraform-as-a-tool-for-infrastructure-as-code-iac/
 
 
### Terraform – Change Automation​
What is Change Management?​

A standard approach to apply change, and resolving conflicts brought about by change.​

In the context of Infrastructure as Code (IaC), Change management is the procedure that will be followed when resources are modified and applied via configuration script.

What is Change Automation?​

a way of automatically creating a consistent, systematic, and predictable way of managing change requests via controls and policies​

Terraform uses Change Automation in the form of Execution Plans and Resources graphs to apply and review complex changesets​

What is a ChangeSet?​

A collection of commits that represent changes made to a versioning repository. IaC uses ChangeSets so you can see what has changed by who over time.​

Change Automation allows you to know exactly what Terraform will change and in what order, avoiding many possible human errors.​

Reference
Running Terraform in Automation
https://learn.hashicorp.com/tutorials/terraform/automate-terraform

###Terraform - Execution Plans​
An Execution Plan is a manual review of what will add, change or destroy before you apply changes eg. terraform apply​

resources and configuration settings will be listed.​

It will indicate will be added, changed​

or destroyed if this plan is approved:​

A user must approve changes by typing: yes​

 ###Terraform – Visualizing Execution Plans​
 
You can visualize an execution plan as a graph using the terraform graph command​

Terraform will output a GraphViz file (you’ll need GraphViz installed to view the file)​

What is GraphViz?​

open-source tools for drawing graphs specified in DOT language scripts having the file name extension "gv"​

###Terraform – Resource Graph​
Terraform builds a dependency graph from the Terraform configurations, and walks this graph to generate plans, refresh state, and more. ​

When you use terraform graph, this is a visual presentation of the dependency graph​

What is a dependency graph?​

In mathematics is a directed graph representing dependencies of several objects towards each other​

Resource Node​​

Represents a single resource​

​Resource Meta-Node​​

Represents a group of resources, but does not represent any action on its own​

​Provider Configuration Node​​

Represents the time to fully configure a provider​

Reference
Resource Graph
https://www.terraform.io/internals/graph


###Terraform — Use Cases​
IaC for Exotic Providers ​

Terraform supports a variety of providers outside of GCP, AWS, Azure and sometimes is the only provider. ​

Terraform is open-source and extendable to any API that could be used to create IaC tooling for any kind of cloud platform or technology. E.g. Heroku, Spotify Playlists.​

Multi-Tier Applications – Terraform by default makes it easy to divide large and complex applications into isolated configuration scripts (module). It has a complexity advantage over cloud-native IaC tools for its flexibility while retaining simplicity over Imperative tools.​

Disposable Environments – Easily stand up an environment for a software demo or a temporary development environment​

Resource Schedulers – Terraform is not just defined to the infrastructure of cloud resources but can be used to dynamic schedule Docker containers, Hadoop, Spark, and other software tools. You can provision your own scheduling grid.​

Multi-Cloud Deployment – Terraform is cloud-agnostic and allows a single configuration to be used to manage multiple providers, and to even handle cross-cloud dependencies.​

Reference
Multi-Cloud Deployment
https://www.terraform.io/intro/use-cases#multi-cloud-deployment

###Terraform Core and Terraform Plugins​
Terraform is logically split into two main parts: ​

Terraform Core​

uses remote procedure calls (RPC) to communicate with Terraform Plugins​
Terraform Plugins​

expose an implementation for a specific service, or provisioner​
Terraform Core is a statically-compiled binary written in the Go programming language.​

Reference
How Terraform Works With Plugins
https://www.terraform.io/plugin/how-terraform-works

Perform CRUD Operations with Providers
https://learn.hashicorp.com/tutorials/terraform/provider-use

### Terraform Up and Running​
Terraform Up & Running takes a deep dive into the internal workings of Terraform.​

If you want to go beyond this course for things like:​

Testing your Terraform Code​
Zero-Downtime Deployment​
Common Terraform Gotchas​
Composition of Production Grade Terraform Code​
Yevgeniy ("Jim") Brikman is the co-founder of Gruntwork​

Reference
Terraform: Up & Running

### Terraform Best Practices
Terraform is an online open-book about Terraform Best Practices​

https://www.terraform-best-practices.com

 ###Github Repo for all Terraform labs:
https://github.com/ExamProCo/Terraform-Associate-Labs

Note: To complete the lab and earn a star, please click on all checkboxes.

### Terraform Install

https://learn.hashicorp.com/tutorials/terraform/install-cli

###Terraform Provisioners​
Terraform Provisioners install software, edit files, and provision machines created with Terraform​

Terraform allows you to work with two different provisioners:​

cloud-init

Cloud-Init is an industry-standard for cross-platform cloud instance initializations. When you launch a VM on a Cloud Service Provider (CSP) you’ll provide a YAML or Bash script.​

Packer

Packer is an automated image-builder service. You provide a configuration file to create and provision the machine image and the image is delivered to a repository for use.​

Provisioners should only be used as a last resort. For most common situations there are better alternatives.​

Create your own Cloud-Init script​

Define the template file​

Reference it in the userdata for the Virtual Machine​

Terraform use to directly support third-party Provisioning tools in the Terraform language Support was deprecated because Terraform considered using Provisioners to be poor practice suggesting better alternatives. ​

Cloud-Init supports Chef and Puppet, so you can just use Cloud-Init​

It is uncertain if this advice extends to Ansible. ​

Terraform and Ansible has lots of learning materials on how their technologies complement each other.​

Reference
Provisioners



