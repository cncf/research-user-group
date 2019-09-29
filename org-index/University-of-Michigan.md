# University of Michigan - Advanced Research Computing and Technology Services

- **Date:** 2019-09-29
- **Contact:** rkillen'@'umich.edu
- **Site:** http://arc-ts.umich.edu

---

## Organization description

**What is your organization? (name, description, mission)**

Advanced Research Computing – Technology Services (ARC-TS) provides research
computing resources to The University of Michigan research projects and their
collaborators. ARC-TS provides High Performance Computing, machine learning,
storage, data, private/public cloud analytical resources, along with a breadth
of outreach and training services.



**Do you consider your group or organization a “traditional” HPC site?**

Yes. ARC-TS has multiple traditional HPC offerings that make up the majority of
it's computational and staff resources.



**How many researchers does your organization have? or how many is your group
supporting?**

8000 faculty members along with their additional support staff and students.



**What areas of research are you primarily supporting using Kubernetes? (e.g.
bioinformatics, physics, generic research platform)**

ARC-TS serves as a general research support group for the University.



**Are your researchers consuming Kubernetes directly (deploying Kubernetes
themselves / using kubectl to access etc)? or do they consume services deployed
on top of it?**

Both. Our researchers fall into 3 categories of users:
1. Those that request ARC-TS runs something on their behalf.
2. Those that don't want access to Kubernetes directly, but want to control how
   their application is deployed and updated. They are given a git repo that
   will auto-update their deployment when items are merged into the master
   branch.
3. Direct access via `kubectl`. They are limited to a single namespace with 
   [Resource Quotas] and [Pod Security Policies] in place. 



**Do you allow your users to deploy their own applications from the internet or
other sources? If so, do you have some sort of vetting process?**

In our unrestricted environment, yes. Deployed applications must still meet the
security level enforced by our strict [RBAC] and [Pod Security Policies].

In our restricted data environment all applications are vetted and must use 
our internal image registry.

---

## Why is your organization looking at Kubernetes?

**What motivated you to explore Kubernetes?**

There has been a growing demand to host and run services beyond what would fall
into the realm of "traditional" HPC. That coupled with the surge of container
adoption and the platform agnostic apis and tooling make Kubernetes an ideal
platform to run these services.



**Were you using containers previously before looking at Kubernetes?**

Yes. ARC-TS itself was using docker containers to run services directly on 
hosts before adopting Kubernetes.

Researchers were using a mix of docker containers locally on their system and 
converting to [Singularity] containers for use with ARC-TS's HPC systems. 



**How important is workload portability?**

Variable depending on the research group. It is however, more often than not
becoming a requirement.



**Are you using Kubernetes to support “new” applications or workloads? or are
you migrating traditional workloads?**

Generally new workloads and migrating ones that are more service like, for 
example Jupyter notebooks.



**If you are migrating to Kubernetes, how are you planning to migrate your
traditional workloads?**

We are running both services side-by-side currently and shift over ones that
don't have a large dependency on components that are associated with a more 
traditional environment such as ones that require access to our parallel shared
filesystem.



**What sort of pain points have you experienced with this migration?**

We have avoided the larger pain points by choosing to not migrate workloads that
have a hard requirement on traditional infrastructure or valid posix identities.



**What benefits have there been switching to Kubernetes? or what is it enabling
you to do?**

It has provided an easy means to run workloads that ARC-TS has not been able
to traditionally run in the past; things such as databases workflow engines
and a slew of other services.



**How are you handling training your users to work with Kubernetes?**

We have put together our own [training material] and have setup internal
training sessions targeted generally at support staff, but are opening it up
to more faculty and students going forward.



---

## Describe your environment

**What phase would you consider your Kubernetes environment is in? (e.g. 
Investigating, Development, Production)**

Production.


**How many Kubernetes clusters do you run? What size are they? (total number of
nodes, total core, total ram count)**

3 clusters:
- A "services" cluster that hosts services such and our source control ([GitLab]),
  and authentication provider ([Keycloak]).
  -  5 nodes, 4 cores / 16GB ram each - 20 cores / 80GB ram total.
- Unrestricted data cluster.
  - 12 nodes, 6 cores / 48GB ram each - 72 cores / 576GB ram total.
- Restricted data cluster (HIPAA etc).
  - 6 nodes, 4 cores / 16GB ram each - 24 cores / 96GB ram total.


**Where are you running your clusters? on-prem? a Cloud Provider? a mixture of 
both? If on-prem, are you running them on bare-metal?**

On-prem. They are virtual and run on top of a kvm based hypervisor.



**What version(s) of Kubernetes are you running?**

v1.14.6 - Our general policy is to remain 1 minor version behind the upstream
stable release.



**What distribution of Kubernetes are you running (Openshift, Rancher etc)?**

No distribution. Our clusters are based off upstream directly.



**What container runtime(s) are you using?**

[Docker-CE]- Our container hosts run on the [Container Linux] OS, which comes 
packaged with docker-ce.



**What CNI driver(s) are you using?**

[Cilium] - Cilium was chosen for it's advanced features such as
[dns based network policies],  and usage of the
[Berkeley Packet Filter (BPF)][bpf]/[Express Data Path (XDP)][bpf].



**How are you provisioning your cluster(s)?**

With [kubeadm] and some additional scripts to automate the node joining process.



**Do you provide persistent storage? If so, how?**

Yes. We use a mixture of [local] storage and shared via the
[NFS-Client Storage Provisioner]



**If you are exposing cluster services externally, how? (service type
`LoadBalancer`, ingress etc.)**

Using [metallb] in [layer-2 mode] to provide an IP Pool for use with
`LoadBalancer` service types along with cluster wide
[Nginx based Ingress controllers]



**In any of your clusters, are you using devices (e.g. GPUs)? If so, what are
they?**

Not at this time. Looking to use them in a future bare-metal cluster.


**What types of workloads are you deploying on top of Kubernetes? HPC, HTC, or
services such as Argo, or JupyterHub?**

Mostly services with a mixture between [JupyterHub], databases, custom
applications and various workflow engines.



---

## Workload managers

**Does your group run other workload managers? (SLURM, HTCondor etc)  If so,
what size cluster(s) do you have supporting those other workload managers?**

Yes, our [Great Lakes] cluster is [SLURM] based with 13,000 cores and 77TB of ram.



**Are you considering running another workload manager on top of Kubernetes? or
pursuing running them natively on Kubernetes?**

Yes, but only for experimental purposes at this time.



**Have you integrated with more traditional environments? e.g. posix/parallel
shared file systems etc?**

Yes, but only in a non-production proof of concept mode.



---

## Multi-tenancy and security

**Do you run or are looking to run restricted data workloads? (HIPAA, PCI etc)**

Yes. Our restricted data cluster supports HIPAA workloads. 



**Is multi-tenancy important to you?**

Yes. We currently operate a shared cluster, and while we have been able to make
it work well for our unrestricted cluster having more defined separation would
help in expanding usage for our restricted data cluster.



**If you have a multi-tenant environment, what methods are you using to
separate your workloads? (e.g. separate clusters / separate namespaces)**

Our clusters are separated based on data classification they serve. Our
restricted data cluster allows for co-location of services, but only
administrators are given direct access.

In our unrestricted data cluster research groups are separated by namespace and
have various policies configured to prevent clashing.



**How are you handling authentication and user management?**

We use [Keycloak] to serve as an [OIDC provider]. It in turn communicates with
our campus wide LDAP.



**How are you handling access control? RBAC? ABAC? Additional tooling?**

[RBAC] and [Pod Security Policies]. We are evaluating [Open Policy Agent] for
further fine grained control.


**Have you explored multi-cluster or federated deployments? If you are actively
using it, what route did you go with which tools?**

Yes, as a part of the [SLATE-CI] project. We looked at and deployed
[Federation-v1], but moved towards custom tooling.



## Workflow technologies, runners, platforms, and/or standards

**(Here we use the word "workflow" to mean batch-style data analysis workflows,
not business process workflows)**

**Do your researchers run workflows at your site?**

Yes. Both on top of Kubernetes and using our HPC Cluster.


**Does your site support particular workflow technologies such as specific
frameworks, runners, platforms, and/or standards?**

Within Kubernetes, we support [Argo] and some of our users have adopted
[GitLab CI][GitLab].

On our HPC system, we don't directly support any workflow systems, but
researchers have adopted or manage their own (e.g. [Snakemake])


**In the future, do you plan to directly support particular workflow technologies
such as specific frameworks, runners, platforms, and/or standards?**

Nothing currently planned. It will be driven by Researcher request.


[Resource Quotas]: https://kubernetes.io/docs/concepts/policy/resource-quotas/
[Pod Security Policies]: https://kubernetes.io/docs/concepts/policy/pod-security-policy/
[singularity]: https://sylabs.io/singularity/
[rbac]: https://kubernetes.io/docs/reference/access-authn-authz/rbac/
[training material]: https://github.com/mrbobbytables/k8s-intro-tutorials
[GitLab]: https://about.gitlab.com/
[Keycloak]: https://www.keycloak.org/
[docker-ce]: https://docs.docker.com/install/overview/
[container linux]: https://coreos.com/os/docs/latest/
[cilium]: https://cilium.io/
[dns based network policies]: https://docs.cilium.io/en/stable/gettingstarted/dns/
[bpf]: https://docs.cilium.io/en/latest/bpf/
[kubeadm]: https://kubernetes.io/docs/reference/setup-tools/kubeadm/
[metallb]: https://metallb.universe.tf/
[layer-2 mode]: https://metallb.universe.tf/concepts/layer2/
[Nginx based Ingress controllers]: https://kubernetes.github.io/ingress-nginx/
[local]: https://kubernetes.io/docs/concepts/storage/volumes/#local
[NFS-Client Storage Provisioner]: https://github.com/kubernetes-incubator/external-storage/tree/master/nfs-client
[jupyterhub]: https://jupyterhub.readthedocs.io/en/stable/
[great lakes]: https://arc-ts.umich.edu/greatlakes/
[slurm]: https://www.schedmd.com/
[oidc provider]: https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens
[open policy agent]: https://www.openpolicyagent.org/
[slate-ci]: https://slateci.io/
[Federation-v1]: https://kubernetes.io/docs/concepts/cluster-administration/federation/
[Argo]: https://argoproj.github.io/
[Snakemake]: https://snakemake.readthedocs.io/en/stable/