# G-Research

- **Date:** 2019-09-18
- **Contact:** jamie.poole@gresearch.co.uk

---

## Organization description

**What is your organization? (name, description, mission)**

G-Research is a leading quantitative research and technology company based in London. We build and run a large research platform that allows our teams of quantitative researchers to apply scientific techniques to find patterns in large, noisy real-world datasets.

**Do you consider your group or organization a “traditional” HPC site?**

Yes

**How many researchers does your organization have? or how many is your group
supporting?**

< 100 researchers

**What areas of research are you primarily supporting using Kubernetes? (e.g.
bioinformatics, physics, generic research platform)**

Financial research

**Are your researchers consuming Kubernetes directly (deploying Kubernetes
themselves / using kubectl to access etc)? or do they consume services deployed
on top of it?**

Researchers generally use services deployed on top of Kubernetes, while engineering teams interact directly to deliver these services.

**Do you allow your users to deploy their own applications from the internet or
other sources? If so, do you have some sort of vetting process?**

Yes, images are vetted.

---

## Why is your organization looking at Kubernetes?

**What motivated you to explore Kubernetes?**

Migration of workloads to Linux and containerization.

**Were you using containers previously before looking at Kubernetes?**

No

**How important is workload portability?**

Very. One of the things that makes Kubernetes attractive is that we become decoupled from our hardware and its configuration. As a result our workloads should be portable between environments.

**Are you using Kubernetes to support “new” applications or workloads? or are
you migrating traditional workloads?**

Both

**If you are migrating to Kubernetes, how are you planning to migrate your
traditional workloads?**

.NET Core enabling Linux migration in general, as well as breaking up monoliths into smaller migratable pieces.

**What sort of pain points have you experienced with this migration?**

AuthN/AuthZ patterns are different when migrating from Windows to Linux. Most pain points have been around this rather than anything specific to Kubernetes.

Migration of services is now a well understood problem, but we do not yet have a clear strategy for migrating batch jobs.

**What have been the benefits of switching to Kubernetes? or what is it enabling
you to do?**

All the standard benefits of Kubernetes and containers:

- Portable workloads
- Automated infrastructure
- Speed of deployment
- Workloads shielded from maintenance of the underlying hardware
- More efficient use of physical resources
- Platform benefits around application lifecycle management / logging / monitoring

**How are you handling training your users to work with Kubernetes?**

Internal and external training courses.

---

## Describe your environment

**What phase would you consider your Kubernetes environment is in? (e.g. 
Investigating, Development, Production)**

We have many Kubernetes clusters running production workloads.

**How many Kubernetes clusters do you run? What size are they? (total number of
nodes, total core, total ram count)**

Order of 10s of clusters

**Where are you running your clusters? on-prem? a Cloud Provider? a mixture of 
both? If on-prem, are you running them on bare-metal?**

On-prem, both virtual and bare-metal.

**What version(s) of Kubernetes are you running?**

Mixture, but within the last couple of major releases.

**What distribution of Kubernetes are you running (Openshift, Rancher etc)?**

N/A

**What container runtime(s) are you using?**

Docker

**What CNI driver(s) are you using?**

Calico

**How are you provisioning your cluster(s)?**

Mixture of custom orchestration and Terraform.

**Do you provide persistent storage? If so, how?**

Via external distributed storage solutions compatible with Kubernetes.

**If you are exposing cluster services externally, how? (service type
`LoadBalancer`, ingress etc.)**

External load balancers and ingress controllers.


**In any of your clusters, are you using devices (e.g. GPUs)? If so, what are
they?**

GPUs

**What types of workloads are you deploying on top of Kubernetes? HPC, HTC, or
services such as Argo, or JupyterHub?**

Many in-house and off-the-shelf services. Starting to explore HTC.

---

## Workload managers

**Does your group run other workload managers? (Slurm, HTCondor etc)  If so,
what size cluster(s) do you have supporting those other workload managers?**

HTCondor.

**Are you considering running another workload manager on top of Kubernetes? or
pursuing running them natively on Kubernetes?**

Natively on Kubernetes if possible, or creating software to allow us to do this.

**Have you integrated with more traditional environments? e.g. posix/parallel
shared file systems etc?**

Yes

---

## Multi-tenancy and security

**Do you run or are looking to run restricted data workloads? (HIPAA, PCI etc)**

No

**Is multi-tenancy important to you?**

Yes

**If you have a multi-tenant environment, what methods are you using to
separate your workloads? (e.g. separate clusters / separate namespaces)**

Namespaces for groups of users, clusters for environment of workload (e.g. sandbox /staging / production)

**How are you handling authentication and user management?**

Custom integration using LDAP as a user store.

**How are you handling access control? RBAC? ABAC? Additional tooling?**

Extensive use of RBAC.

**Have you explored multi-cluster or federated deployments? If you are actively
using it, what route did you go with which tools?**

We handle our own deployment to multiple clusters. We have written some tools to integrate with and external Consul infrastructure for service discovery.

## Workflow technologies, runners, platforms, and/or standards

**(Here we use the word "workflow" to mean batch-style data analysis workflows,
not business process workflows)**

**Do your researchers run workflows at your site?**

Yes

**Does your site support particular workflow technologies such as specific
frameworks, runners, platforms, and/or standards?**

Yes, mostly built in-house.

**In the future, do you plan to directly support particular workflow technologies
such as specific frameworks, runners, platforms, and/or standards?**

Yes, as above plus more integration with community tools.
