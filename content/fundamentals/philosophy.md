---
title: "Philosophy"
description: "Learn more about the core philosophy and principles that make up the SweetOps methodology."
weight: 2
---

SweetOps is built on a foundational philosophy that ensures the methodology is comprehensive and reusable across organizations. To fully understand what SweetOps is and how to utilize it effectively, it's critical to understand the backing principles that define it.

## 100% Open Source

All of the primary technology that enables SweetOps is Open Sourced by [Cloud Posse](https://cloudposse.com) and the community under Apache 2.0 Open Source Software License. Using open source licensing is a practical, deliberate strategy. It enables SweetOps to be easily adopted by organizations by using a well-understood license that carries less risk than proprietary licenses. With SweetOps, everything is permissively licensed, which makes Infrastructure as Code more straightforward to adopt. It protects all parties to reuse the software and fosters greater collaboration.

## Automate Everything

An important idea from the beginning has been to ensure that all pieces of the process are automated. This includes everything from AWS account creation to configuring incident response management tooling. Ensuring that all aspects of SweetOps are automated makes processes repeatable, transparent, and reliable without having to depend on quickly outdated documentation (aka WikiOps).

## Embrace the UNIX Philosophy for the Cloud Era

The SweetOps infrastructure as code library, purpose built tools, and reusable catalogs are all crafted to follow the [UNIX Philosophy](https://en.wikipedia.org/wiki/Unix_philosophy); they're intended to be small, simple, readable, and modular in nature which encourages composition.

SweetOps never intends to provide one tool that does it all. It is the polar opposite of platforms like OpenShift and Rancher which attempt to do everything. Instead, SweetOps provides small tools that do one thing well and then stitch them together to achieve the best results. This enables SweetOps to swap in & out tools as better ones come along.

## YAML Configuration Drives As Much As Possible

SweetOps has adopted YAML as its configuration syntax of choice. YAML is a portable, well-understood configuration format that is widely known and accepted within the DevOps community. It easily used in any language and has many advantages over using configuration formats.

Particularly of note is the comparison of YAML to Terraform's `.tfvar` files which are a form of HCL. With `.tfvar` files it is not possible to load them from remote locations (e.g. over `https://`), do interpolations, or control which files we want to load and when to load them. On the other hand, using YAML, we're able to address all of these shortcomings while also supporting [anchors](https://helm.sh/docs/chart_template_guide/yaml_techniques/#yaml-anchors) and permits us to define additional behaviors like imports and inheritance.

Utilizing YAML also enables SweetOps to separate code from configuration. Many will agree that Terraform has graduated from being purely configuration into a full-fledged programming language. With that being the case we focus on putting our business logic into Terraform and keep our configuration separate in YAML. This results in more reusable, clearly configured usage of our tools.

## 4 Layers of Infrastructure
![4 Layers of Infrastructure](https://lucid.app/publicSegments/view/dc705e05-cf3e-4e03-9029-acd8c4b4812f/image.png)

SweetOps breaks down cloud infrastructure into 4 discrete layers:

1. **Foundation**: Your AWS Accounts, VPCs, IAM, and DNS architecture.
1. **Platform**: Your EKS / ECS Clusters, Load Balancers, IAM Service Accounts, and Certificates.
1. **Shared Services**: Your CI/CD pipelines, BeyondCorp solution, and Monitoring and Logging tooling.
1. **Application**: Your Backend and Frontend Applications.

We delineate between these layers as they have different Software Development Life Cycles (SDLC) and tools that are responsible for managing them. For example, Terraform is great for building your Foundation layer, but other tools might be better for managing the continuous delivery of the Application layer (e.g. ArgoCD). It's also important to note that each layer builds on the previous and the lower layers are less likely to change over time. At the bottom, you won't frequently change your AWS accounts and VPCs in your Foundation layer, just like when operating a platform you won't be rebuilding EKS clusters in your Platform layer without disrupting all tenants of the platform. You might, however, add HashiCorp Vault to your Shared Services layer to increase your security posture or add a new API microservice to your Application layer. The Application Layer is ultimately the most important layer of them all: it's what drives your business. It's where your applications live, which is why it will change continuously.

## Optimize for Day 2 Operations

One important part we emphasize within SweetOps is that we optimize the methodology for [day 2+ operations](https://dzone.com/articles/defining-day-2-operations) and not the cold-start. The process to create the bottom layers of your platform is day 1 or your cold-start process. You will generally only perform a cold-start once so it's not logical or economical to focus on agility in this phase of building the platform. Instead, SweetOps focuses on optimizing the processes that come after your cold-start: GitOps, release engineering, monitoring/SRE, and ensuring your applications run efficiently on top of the base platform.

## Share Nothing

SweetOps takes the principle of [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns) to heart when it comes to infrastructure. We believe strongly in fine grained separations of AWS Accounts, AWS Organizational Units, environments, and access credentials. We utilize a separate AWS account to manage DNS, logs, auditing, and identity in practice of this principle. These practices ensure optimal security and agility if any part of the system is compromised or needs to
change in some way.

## Secure by Default

The SweetOps infrastructure as code library focuses on being secure by default rather than requiring additional configuration to secure it. We think about this as being implicitly secure and if your use-case requires insecurity for one reason or another then you need to be explicit about that.

One way we practice our "Secure by Default" process is by utilizing [BridgeCrew](https://bridgecrew.io/)'s security scanning tools [on our Terraform modules and components](https://github.com/Cloudposse/terraform-aws-vpc#security--compliance-) to ensure they're passing many of the leading security compliance testing frameworks.

## Delegate Thought Leadership

As much as possible, SweetOps aims to identify thought leaders and mimic them instead of reinventing the wheel with our own solutions. This is why SweetOps chooses to use best in class tools like Terraform, Helmfile, ArgoCD, etc. Instead of creating those types of tools ourselves, we aim to provide the thought leadership on how to tie and orchestrate those tools together (e.g. via [Stacks]({{< relref "fundamentals/concepts.md#stacks" >}})).
