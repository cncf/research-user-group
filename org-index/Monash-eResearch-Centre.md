# Monash eResearch Centre

- **Date:** 2019-09-11
- **Contact:** brett.milford'@'monash.edu
- **Site:** https://www.monash.edu.au/eresearch/

---

## Organization description

**What is your organization?**

Monash eResearch Centre is a University commitment to enabling and accelerating research
through the application of advanced computing, data informatics, tools and
infrastructure, delivered at scale, and built with a co-design principle between
researchers and technologists.

**Do you consider your group or organization a “traditional” HPC site?**

No. Monash eResearch Centre provides other infractructue and services in addition to
traditional HPC/HTC clusters:

- [MASSIVE]/MonARCH - Cloud based batch computing facilities suited to data
  centric research including HPC,HTC & GPU intensive applications.
- [CVL] - A platform for integrating tools, resources, and data for researchers.
Research Data Services - Comprised of mutiple infrastructure tiers and services
including a 14 Petabyte Ceph cluster for online storage.
- R@CMon/[NeCTAR] - The Australian Research cloud, designed for federated access to self-service computing and
storage infrastructure for building bespoke systems and engaging in cross-institution collaboration.


**How many researchers does your organization have? or how many is your group
supporting?**

Approximately 10000 researchers, comprised of faculty members, students and
support staff both within Monash and from partner institutions.


**What areas of research are you primarily supporting using Kubernetes? (e.g.
bioinformatics, physics, generic research platform)**

- Bioinformatics 
- Information & Computing Sciences
- Medicine & Health Sciences
- Pharmacology
- Mathematical Sciences

[And many more]

**Are your researchers consuming Kubernetes directly (deploying Kubernetes
themselves / using kubectl to access etc)? or do they consume services deployed
on top of it?**

Most of our users are currently deploying and consuming Kubernetes directly
either manually or via [Magnum]. Some are consuming services such as
[JupyterHub] on top of Kubernetes.


**Do you allow your users to deploy their own applications from the internet or
other sources? If so, do you have some sort of vetting process?**

On unmanaged resources (e.g. self-service cloud infrastructure) Yes. No we do
not have a vetting process.

---

## Why is your organization looking at Kubernetes?

**What motivated you to explore Kubernetes?**

- In response to uptake and demand from users.
- As a way of increasing the utilisation of infrastructure & efficiencies in scheduling.
- As part of a wider service offering of tools for researcher work-flows.
- As a method of improving portability of users workloads across systems and infrastructures.

**Were you using containers previously before looking at Kubernetes?**

Yes:
- As part of a Application catalogue ([Murano] Applications).
- Software and configuration management for HPC applications (Singularity).

**How important is workload portability?**

Very important - Most of our user support challenges are in this space.

**Are you using Kubernetes to support “new” applications or workloads? or are
you migrating traditional workloads?**

Both

**If you are migrating to Kubernetes, how are you planning to migrate your
traditional workloads?**

By running both side by side, Applications and use cases amenable to 
Kubernetes deployment would be the first to trial & move.


**What sort of pain points have you experienced with this migration?**

N/A

**What have been the benefits of switching to Kubernetes? or what is it enabling
you to do?**

N/A

**How are you handling training your users to work with Kubernetes?**

N/A

---

## Describe your environment

**What phase would you consider your Kubernetes environment is in? (e.g. 
Investigating, Development, Production)**

 Mostly Investigating with some use cases and instances in development and production.

**How many Kubernetes clusters do you run? What size are they? (total number of
nodes, total core, total ram count)**

2 clusters in production.
4 In development/testing.

Approximately (across all clusters):
- Nodes: 86
- Cores: 194
- RAM: 544

**Where are you running your clusters? on-prem? a Cloud Provider? a mixture of 
both? If on-prem, are you running them on bare-metal?**

On-prem cloud provided by OpenStack.

**What version(s) of Kubernetes are you running?**

1.15.2

**What distribution of Kubernetes are you running (Openshift, Rancher etc)?**

Canonical K8s

**What container runtime(s) are you using?**

Docker

**What CNI driver(s) are you using?**

- Flannel
- Calico

**How are you provisioning your cluster(s)?**

- Ansible
- [k8s-on-openstack] (Ansible)
- Magnum

**Do you provide persistent storage? If so, how?**

Cinder (Ceph) RBD volumes

**If you are exposing cluster services externally, how? (service type
`LoadBalancer`, ingress etc.)**

Cloud based clusters are utilising load balancers provided from Neutron (with
the Midonet L3 driver).

**In any of your clusters, are you using devices (e.g. GPUs)? If so, what are
they?**

N/A

**What types of workloads are you deploying on top of Kubernetes? HPC, HTC, or
services such as Argo, or JupyterHub?**

- In house applications e.g. [MyTardis]
- Juypter Hub

---

## Workload managers

**Does your group run other workload managers? (SLURM, HTCondor etc)  If so,
what size cluster(s) do you have supporting those other workload managers?**

Slurm

**Are you considering running another workload manager on top of Kubernetes? or
pursuing running them natively on Kubernetes?**

Not currently.

**Have you integrated with more traditional environments? e.g. posix/parallel
shared file systems etc?**

Not yet.

---

## Multi-tenancy and security

**Do you run or are looking to run restricted data workloads? (HIPAA, PCI etc)**

Yes, in the future.

**Is multi-tenancy important to you?**

Yes, a degree of multi-tenancy is provided by our IaaS layer - in the future
this may need to be catered for in Kubernetes.

**If you have a multi-tenant environment, what methods are you using to
separate your workloads? (e.g. separate clusters / separate namespaces)**

Openstack provides multi-tenancy & federated access - individual clusters are usually deployed within these tenants.

**How are you handling authentication and user management?**

N/A

**How are you handling access control? RBAC? ABAC? Additional tooling?**

N/A

**Have you explored multi-cluster or federated deployments? If you are actively
using it, what route did you go with which tools?**

N/A


[MASSIVE]: https://www.massive.org.au/
[CVL]: https://www.cvl.org.au/
[NeCTAR]: https://nectar.org.au
[And many more]: https://nectar.org.au/about/impact-and-usage/fields-research-codes/
[Magnum]: https://wiki.openstack.org/wiki/Magnum
[JupyterHub]: https://sphpm.erc.monash.edu/
[Murano]: https://wiki.openstack.org/wiki/Murano
[k8s-on-openstack]: https://github.com/infraly/k8s-on-openstack
[MyTardis]: https://github.com/mytardis/mytardis/
