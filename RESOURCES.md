# Resources and Links


## Large Clusters and Scaling

 - [Scaling Kubernetes to 2,500 Nodes](https://openai.com/blog/scaling-kubernetes-to-2500-nodes/) -
   A blog post from the OpenAI team on some of the issues and best practices
   associated with running large scale Kubernetes clusters.

## Software, Frameworks and Collections

### Software
- [Volcano](https://volcano.sh) - A Kubernetes native batch scheduler. Adds
  support for MPI, fair-share, queues and more.
- [Kubeflow](https://www.kubeflow.org/) - Tightly integrated collection of
  _"best of breed"_ software for Machine learning.
- [Zero to JupterHub](https://zero-to-jupyterhub.readthedocs.io/en/latest/) -
  Helm Chart for Jupyterhub maintained by upstream Jupyterhub community.
- [Armada](https://github.com/G-Research/armada) - A multi-cluster batch scheduler for high-throughput workloads on Kubernetes

### Frameworks
- [Hierarchical Namespace Controller](https://github.com/kubernetes-sigs/multi-tenancy/tree/master/incubator/hnc) -
  Kubernetes Multi tenancy Working Group project to provide "nested" namespaces,
  and propagate RBAC policies, secrets etc.

### Research Institution Collections
- [CERN Helm Chart Collection](https://gitlab.cern.ch/helm/charts/cern) -
  Includes: JupyterHub, eosxd, jupyterhub, kube-monkey, ntpd, prometheus, squid
  and sssd. (2019-11-3)
- [PNNL Misc(ellaneous) Scripts (Helm and others)](https://github.com/pnnl-miscscripts/miscscripts)
