---
Title: Infrastructure As Code
Date Created: 27-March-2026
Last Updated: 12-April-2026
Tags:
  - CS5224
  - SWE/CloudComputing/IaC
---
# Infrastructure
---
We understand what infrastructure is based on [[Year 3/Sem 2/CS5224 - Cloud Computing/Cloud Concepts & Models.md#Infrastructure As a Service|infrastructure as a service]]. Essentially we are <b><span style='color: #FFD700'>focusing on the hardware</span></b> such as:
- Virtual machines
- Databases
- Networks
- Load-balancer
## Managing Infrastructure

So typically how do we (*the consumers*) **manage infrastructure**, there are 2 methods:
1) Graphical user interface (*basically a dashboard*)
2) Command line (*writing scripts to analyse your cloud*)

>[!fail] These techniques or managing infrastructure in general have many issues
>- It is <b><span style='color: var(--mk-color-red)'>very manual</span></b> & is <b><span style='color: var(--mk-color-red)'>time consuming</span></b> (*especially GUI where the UI can change*)
>- <b><span style='color: var(--mk-color-red)'>Complex & error-prone</span></b> if your infrastructure itself is complicated
>- Scalability means <b><span style='color: var(--mk-color-red)'>more things to manage & observe</span></b>
>- <b><span style='color: var(--mk-color-red)'>Configuration drift</span></b> (*did not update infrastructure & thus making them out of date*)

>[!hint] We want to manage infrastructure as if we are writing a program
>This is where the term <b><span style='color: #87CEEB'>infrastructure as code</span></b> comes from.
>
>>[!abstract] Infrastructure as Code
>>Ability to <b><span style='color: #FFD700'>provision & support your computing infrastructure using code</span></b> instead of manual processes and settings.
>>
>>So it is like some <b><span style='color: #FFD700'>template to manage infrastructure</span></b>.

**Why do we use code** to manage infrastructure, it is because we can <b><span style='color: #FFD700'>use some of the best practices from software development</span></b>:
- Version control (*what changes were done because its all in code*)
- CI/CD pipelines (*code is regularly tested & deployed*)
- Testing
- Documentation (*how things work and also easily understand how to setup other infrastructure, like moving from AWS to GCP*)
# Infrastructure As Code
---
So now you can think of infrastructure as code (*IaC*) as part of [[Year 2/Sem 1/CS2103 - Software Engineering/Project Management.md#Software Development Life Cycle|SDLC]] or a <b><span style='color: #FFD700'>key element in</span></b> [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Software Engineering Processes.md#DevOps|DevOps]] to <b><span style='color: #98FB98'>bridge the gap between development & operations</span></b> (*development & IT operations like maintenance and observation*).

>[!success] Benefits of IaC in DevOps
>- <b><span style='color: #98FB98'>Automate infrastructure setup</span></b> as we can do all this in code
>- Have <b><span style='color: #98FB98'>rapid deployment</span></b>
>- <b><span style='color: #98FB98'>Repeatable & consistent</span></b>, the code is repeatable and deterministic in both good & bad scenarios  (*just use an infrastructure template*)
>- <b><span style='color: #98FB98'>Easy scalability</span></b>

>[!fail] Pitfalls of IaC
>- Steep learning curve (*basically learning a new the tool*)
>- Large number of tools
>- Code complexity (*it is not simple code to set everything up*)
>- Version control (*working on outdated versions*)
>- Configuration drift
>- Code security (*anyone can take the code & mess things up or leak it*)

But moving forward for the **future of IaC**:
- **Using AI** to deploy and manage
- **Policy-as-code** (*PaC*) making IaC essentially policy-aware to comply with regulations
- **Rise of GitOps**, automatically deploy changes
- **Self-healing IaC**, the code is checked to detect anomalies & update as necessary
- **Multi-cloud functionality**
## Implementing IaC in DevOps

We can **seamlessly implement IaC** by just <b><span style='color: #FFD700'>integrating to our</span></b> [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Engineering Principles & Patterns.md#Continuous Integration & Deployment|CI/CD]] pipelines. This **pipeline** essentially tests (*spin up a production-like environment*) and deploys our code.

If we **integrate IaC in the pipeline**, then you can <b><span style='color: #FFD700'>manage & update your infrastructure when necessary automatically</span></b> (*along with deployment of code & other stuff*).

You can also **improve testing of infrastructure** by <b><span style='color: #FFD700'>setting up environments & tearing it down</span></b> easily in code.

>[!success] By doing this it supports team collaboration
>Now <b><span style='color: #FFD700'>everything is within the same repository</span></b> or in the same area. **Typically infrastructure and code are seperate**.
>
>So by putting everything in one place, developers and IT operations can work together.

So now **what do we code** in our templates? There are **2 approaches** you can take:
1) **Imperative**

This is more like a <b><span style='color: #FFD700'>task management</span></b> method. Where you <b><span style='color: #FFD700'>instruct the exact steps to set up the infrastructure</span></b>.

>[!fail] The developer now needs to track & understand more things
>Because you need to know what you need, steps to take to set everything up & manage changes if needed.

2) **Declarative**

This is more like a <b><span style='color: #FFD700'>state management</span></b> method. Where you <b><span style='color: #FFD700'>state the necessary state of the infrastructure</span></b> then the <b><span style='color: #98FB98'>infrastructure will automatically handles everything</span></b> (*setup, updates, changes*).
## IaC Tools

### Cloud Providers

>[!important] These tools are only specific to that infrastructure
>Meaning it the tool is from AWS it only works on AWS infeastructure.

>[!failure] When using different IaC cloud tools you need to learn completely new things
>This is because they <b><span style='color: var(--mk-color-red)'>do things differently</span></b> as you can see when we explore the different tools.

There are **3 popular ones**:
1) **AWS CloudFormation & CDK**

These are **2 different tools**, first the <b><span style='color: #87CEEB'>AWS cloud development kit</span></b> (*AWS CDK*). Essentially it is the <b><span style='color: #FFD700'>cloud application resources defined as programming languages</span></b> & configuration tools all in the IDE. 

For the AWS <b><span style='color: #87CEEB'>CloudFormation</span></b> which is the same where we manage cloud resources published in the CloudFormation registry, the developer community, and internal libraries.

But it is typically <b><span style='color: #FFD700'>done in a JSON or YAML format</span></b>.

2) **Azure Resource Manager**

It <b><span style='color: #FFD700'>provides a management layer over the infrastructure</span></b>. So this resource manager <b><span style='color: #FFD700'>provides ways to engage with the management layer</span></b> (*then it will take care of the rest*).

![[Azure Resource Manager Overview.png|center]]

All this is done through <b><span style='color: #FFD700'>declarative templates</span></b> (*just tell the state*). Then Azure will <b><span style='color: #FFD700'>manage all these resources as a group</span></b>.

>[!success] Re-deployability
>Their declarative templates will ensure that redeployment of resources will be in a consistent state.

>[!note] Azure has role based access through Azure RBAC
>It is essentially a role based authentication on what can you configure.

3) **Google Infrastructure Manager**

So previously google uses its google cloud deployment manager which is ending their support soon! (*30 march 2026*). But they are migrating to this infrastructure manager (*because GCP has complex and hard to use*).

But essentially it <b><span style='color: #FFD700'>automates the deployment and management of Google Cloud Infrastructure</span></b>, which uses [[Year 3/Sem 2/CS5224 - Cloud Computing/Infrastructure As Code.md#Terraform|Terraform]]:
- <b><span style='color: #FFD700'>Terraform configuration</span></b> defines the infrastructure
- Configuration is <b><span style='color: #FFD700'>deployed onto Google Cloud by Infra Manager</span></b>

**Application deployment** is done via <b><span style='color: #87CEEB'>Cloud Build</span></b> and <b><span style='color: #87CEEB'>Cloud Deploy</span></b> (*third party tools* *can also be used*).
### Independent Tools

>[!important] These tools work across different cloud providers
#### Terraform

It is open-source, though under a Business Source Licence from 2023.

It can be used to <b><span style='color: #FFD700'>manage complex, multi-cloud infrastructure</span></b>.

>[!abstract] Terraform language
> It is a <b><span style='color: #FFD700'>declarative language</span></b> & it uses <b><span style='color: #87CEEB'>HashiCorp configuration language</span></b> (*HCL*).
> 
> This language is used to <b><span style='color: #FFD700'>declare resources or infrastructure</span></b>.

>[!failure] You might need to spend time to learn this new syntax or language
>It is not just some simple JSON or Markdown.

>[!success] It is cloud agnostic
>It supports a large list of cloud providers.

Essentially it is a <b><span style='color: #FFD700'>state machine</span></b>, how it works is that it creates & manages resources on cloud platforms <b><span style='color: #FFD700'>through the use of APIs</span></b>.

>[!info] So essentially Terraform takes your input & transform it and call the correct API from the providers to set up the infrastructure
>So the community & the providers have provided the code to allow you to do this. Their registry contains all the different providers.

**Overview of Terraform's workflow**
![[Terraform Core Workflow.png|center]]
##### Terraform Configuration

This configuration **tells** Terraform <b><span style='color: #FFD700'>how to manage a given collection of infrastructure</span></b>.

>[!note] This can be in multiple files & directories

The syntax consist of only a **few basic elements**:
- Blocks
- Arguments
- Expressions

>[!example] Example to create an AWS S3 bucket
> ```json
> // This is a block, containting 1 block type & 0 or more lables
>resource "aws_s3_bucket" "example" {
>// The variable name is argument, expressions are values
bucket = "my-tf-test-bucket"
tags = { // Attributes for the bucket
>	Name = "My bucket" // This an argument
>	Environment = "Dev"
>	}
}
>```
##### State File

This is the core of the workflow where it <b><span style='color: #FFD700'>keeps track of the infrastructure as a state</span></b> (*that's why we mention that Terraform is a state machine*).

And to **automate changes** (*from 1 state to another*), it <b><span style='color: #FFD700'>builds a resource graph</span></b> to determine resource dependencies & creates or <b><span style='color: #98FB98'>modifies non-dependent resources in parallel</span></b> (*the process is fast*).

It also has <b><span style='color: #98FB98'>standardize configurations</span></b>, supporting <b><span style='color: #98FB98'>reusable configuration</span></b> components called <b><span style='color: #87CEEB'>modules</span></b> (*by Terraform or write your own*) that define <b><span style='color: #FFD700'>configurable collections of infrastructure</span></b>.

It also allows for <b><span style='color: #98FB98'>collaboration</span></b>. In the end <b><span style='color: #FFD700'>these are all files</span></b> which can be added to a version control system.

>[!note] For a bigger team you can collaborate using HCP Terraform
>Its their cloud platform for Terraform where you can effectively manage workflow across teams.
#### Pulumi

So in Terraform it uses their own language and converting it into something else, so why not <b><span style='color: #FFD700'>specify in any language, interpret & convert</span></b>.

So Pulumi **supports languages** like <b><span style='color: #DDA0DD'>TypeScript</span></b>, <b><span style='color: #DDA0DD'>Python</span></b>, <b><span style='color: #DDA0DD'>Go</span></b> & <b><span style='color: #DDA0DD'>C#</span></b>. And with programming languages, Pulumi has the <b><span style='color: #FFD700'>flexibility to handle more complex logic</span></b> (*for loops to make multiple storages for instance*).

And as an added feature it is <b><span style='color: #FFD700'>compatible with Agentic AI</span></b> (*Pulumi Neo*).