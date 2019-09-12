# CERN

- **Date:** 2019-09-11
- **Contact:** ricardo.rocha@cern.ch

---

## Organization description

**What is your organization? (name, description, mission)**

CERN is the European Organization for Nuclear Research. Its mission is to
provide a unique range of particle accelerator facilities to researchers, to
advance the boundaries of human knowledge. It also provides the required
infrastructure to store and analyse 100s of petabytes of data collected by its
experiments.


**Do you consider your group or organization a “traditional” HPC site?**

While CERN also has traditional HPC cluster deployments, its main use case is
often described as HTC (high throughput computing). The reason for this
distinction is that unlike traditional HPC workloads there are little or no
requirements for interconnectivity and interaction between each workload unit
(job). Our workloads are often described as embarassingly parallel.


**How many researchers does your organization have? or how many is your group
supporting?**

CERN has more than 5000 users on site, but it serves a much larger community of
physicists spread around the world - several 10000s.


**What areas of research are you primarily supporting using Kubernetes? (e.g.
bioinformatics, physics, generic research platform)**

Particle Physics.


**Are your researchers consuming Kubernetes directly (deploying Kubernetes
themselves / using kubectl to access etc)? or do they consume services deployed
on top of it?**

We serve a large variety of use cases, and they include:
* Running centralized Kubernetes services such as JupyterHub or administration
  services where the end user only sees the application and has no direct
  interaction with the cluster
* Running centralized and managed Kubernetes services and multi-tenant
  workloads where end users have access to the API server using kubectl -
  weblogic is a good example
* *Kubernetes as a Service* where users create their own dedicated clusters
  (similar to GKE or AKS) and have full admin access using kubectl. As of today
  this is the most popular option


**Do you allow your users to deploy their own applications from the internet or
other sources? If so, do you have some sort of vetting process?**

For now installing applications from public registries is still allowed,
but work is ongoing to enforce usage of our internal gitlab image registry. We
also plan to enable security scanning on all images, and have tried to also run
live binary scans on our clusters.


---

## Why is your organization looking at Kubernetes?

**What motivated you to explore Kubernetes?**

CERN has focused on distributed computing infrastructures for a long time,
the biggest being the Worldwide LHC Computing Grid (WLCG) which powers the data
processing from the Large Hadron Collider (LHC). Challenges include software
maintenance, upgrades, service monitoring, etc. Simplifying this infrastructure
is a never ending task.

Docker became popular in two areas: simplifying application deployment and
separating the infrastructure from the applications, allowing the former to be
upgraded at a different (and faster) pace. At the same time, some of the
experiments also saw value in Docker as an easier way to achieve reproduceable
analysis.

The first attempts included deployments of Apache Mesos, and later Docker Swarm
and Kubernetes. With time external and internal traction indicated Kubernetes
as the solution that best fits our requirements.


**Were you using containers previously before looking at Kubernetes?**

Yes. Docker usage was widespread both for single machine deployments (laptops
and VMs on our private cloud) and later using Apache Mesos and Docker Swarm as
orchestrators. In some cases users also experimented with their own home grown
container orchestration tools.

Other solutions for containerization being used include Singularity, mostly due
to its ability to run rootless which makes it a good option for shared batch
clusters.


**How important is workload portability?**

Portability is important for use cases showing periodic peaks in resource
requests, which is the case of our physics analysis. Portability should make
bursting to external resources much easier.


**Are you using Kubernetes to support “new” applications or workloads? or are
you migrating traditional workloads?**

Both. Examples of new applications include our reproduceable analysis portals,
notebook services and digital libraries. Examples of migration of traditional
workloads include WebLogic and internal systems like GitLab or JIRA.

The biggest impact is in large scale data analysis where Kubernetes has opened
new deployment options. An example is Spark where the main centralized
deployment is based on Yarn and configured with Puppet, but where
a *Spark as a Service* on top of Kubernetes is also available.


**If you are migrating to Kubernetes, how are you planning to migrate your
traditional workloads?**

In most cases the Kubernetes deployments are at a start additional instances of
existing services - WebLogic, Spark, HTCondor. As the responsible teams gain
confidence with these new deployments, they tend to start migrating also the
remaining capacity to Kubernetes, in a controlled and phased way.


**What sort of pain points have you experienced with this migration?**

There are several challenges with this process:
* Team members need to learn Kubernetes which includes a much more significant
  mindset shift than what happened when transitioning to virtualization
* Learning curve is steep, in the application setup but especially on
  debugging and troubleshooting of both applications and clusters
* Kubernetes expects services available that we cannot easily provide on prem
  today. An example is serviceType LoadBalancer, which was not available in our
  flat network infrastructure and complicates the application ingress setup
* Managing cluster upgrades is not trivial and to minimize impact most teams
  have instead been redeploying their applications in brand new clusters


**What have been the benefits of switching to Kubernetes? or what is it enabling
you to do?**

Our Kubernetes deployments already show huge improvements in areas like:
* Speed of deployment, where we went from hours for a configuration or software
  update to seconds. Even when deploying in a brand new cluster it is usually
  a matter of minutes
* Simplification of our stack, as Kubernetes takes care of the application
  configuration, scheduling, monitoring, restarts and log collection. As we
  also deploy Prometheus in our clusters this also includes metric gathering
* Software maintenance, as we rely on a very large community and contribute to
  a much larger effort, as opposed to maintaining it in house
* API consolidation, which is one of the key benefits of Kubernetes. Having
  a consistent platform on which we now build on allows us to more easily
  maintain a diverse set of application and opens up the possibility to extend
  our on prem resources to external public clouds


**How are you handling training your users to work with Kubernetes?**

We organize internal trainings every few months, covering container basics but
also advanced topics of orchestration, resource allocation, configuration and
auto scaling. We also do internal Container Office Hours where we take
questions from our users and document the answers in a Discourse instance.


---

## Describe your environment

**What phase would you consider your Kubernetes environment is in? (e.g. 
Investigating, Development, Production)**

We have several instances of Kubernetes being used in Production.


**How many Kubernetes clusters do you run? What size are they? (total number of
nodes, total core, total ram count)**

We run over 400 clusters today, in different phases of adoption. The typical
production cluster size is of the order of 10 nodes, each 4 core 8 GB RAM.
For the data processing clusters, they are on the order of 100s of nodes,
each 8 or 16 core and 16 or 32 GB RAM. In total we have over 2000 nodes today.


**Where are you running your clusters? on-prem? a Cloud Provider? a mixture of 
both? If on-prem, are you running them on bare-metal?**

Almost all on prem, with a few exceptions where we attempt to burst our capacity
to public cloud providers. We offer both virtualized and baremetal clusters,
but most run on VMs today.


**What version(s) of Kubernetes are you running?**

As we offer an easy way to deploy Kubernetes by end users, existing clusters
include versions 1.11, 1.12, 1.13, 1.14. We aim to stay close to the latest
release once we are confident with our upgrade process.


**What distribution of Kubernetes are you running (Openshift, Rancher etc)?**

OpenStack Magnum for the *as a service* deployments, with Fedora Atomic as the
host OS. OpenShift for a central PaaS instance.


**What container runtime(s) are you using?**

Docker, but looking into cri containerd. Singularity for HPC and some batch
workloads.


**What CNI driver(s) are you using?**

Flannel.


**How are you provisioning your cluster(s)?**

We rely on OpenStack Magnum for cluster provisioning.


**Do you provide persistent storage? If so, how?**

We offer both CEPH RBD and CephFS, via CSI drivers. The latter is the most
popular option.


**If you are exposing cluster services externally, how? (service type
`LoadBalancer`, ingress etc.)**

We currently do not have a L3 load balancing service in house (though we are
about to offer one), and applications rely on Ingress. We offer Traefik and
Nginx as Ingress controllers, with some users replacing this with HAProxy. This
is due to the different set of functionality offered by each of these tools.


**In any of your clusters, are you using devices (e.g. GPUs)? If so, what are
they?**

We have integrated GPUs in a couple clusters - NVIDIA GPUs managed by the
corresponding device plugin. Two other cases include exposing a specific device
to manage tape drives and a USB security device, but in this case the container
allocation is done manually and the driver is handled by a dedicated container.


**What types of workloads are you deploying on top of Kubernetes? HPC, HTC, or
services such as Argo, or JupyterHub?**

Notebooks with Jupyterhub, HTC and Spark are the most relevant data analysis
workloads being run on Kubernetes today. 


---

## Workload managers

**Does your group run other workload managers? (SLURM, HTCondor etc)  If so,
what size cluster(s) do you have supporting those other workload managers?**

Our main batch farm relies on HTCondor. It is of the order of 200000 cores.


**Are you considering running another workload manager on top of Kubernetes? or
pursuing running them natively on Kubernetes?**

We're looking at running batch workloads directly on Kubernetes, also to allow
an easy way for people to spawn and destroy new clusters on their own quota -
as an alternative to relying on the central batch system. Our requirements
include fair share and workload prioritization, and we've looked at tools such
as kube-batch and volcano, as well as the different federation alternatives.


**Have you integrated with more traditional environments? e.g. posix/parallel
shared file systems etc?**

We offer access to several in-house shared filesystems - EOS, CVMFS, AFS,
CephFS. Where volume provisioning is required we rely on CSI drivers. For the
other cases, we run a DaemonSet on every cluster which sets up the required
fuse mounts.


---

## Multi-tenancy and security

**Do you run or are looking to run restricted data workloads? (HIPAA, PCI etc)**



**Is multi-tenancy important to you?**

Up to now multi-tenancy has been achieve by splitting workloads across
different clusters. As more services move to Kubernetes we expect
a consolidation of these deployments where single cluster multi-tenancy will be
more important.


**If you have a multi-tenant environment, what methods are you using to
separate your workloads? (e.g. separate clusters / separate namespaces)**

We have a few services - digital libraries, puppet masters - where
multi-tenancy is being done using namespaces. For most cases though we do it
via separate clusters today.


**How are you handling authentication and user management?**

We offer two ways:
* TLS based with certificates handling by a cluster specific CA
* OpenStack Keystone tokens, which are integrated with our internal identity
  mechanisms

Internally we rely on ActiveDirectory and have an experimental Keycloak
deployment.


**How are you handling access control? RBAC? ABAC? Additional tooling?**

We rely on RBAC extensively, and have been considering enforcing strict Pod
Security Policies.


**Have you explored multi-cluster or federated deployments? If you are actively
using it, what route did you go with which tools?**

We have been exploring this area for 2 years now. We tried and liked federation
v1 thanks to its simplicity but lacked features like fair share scheduling,
prioritization and the ability to define policies on which clusters workloads
should be directed to. We experimented with federation v2, which tries to
address some of these issues but relies on a new set of resources and does not
seem stable enough right now.

We are also experimenting with custom schedulers and the open policy agent to
address cluster policies setting, as well as virtual kubelets to extend cluster
resources across datacenter boundaries.
