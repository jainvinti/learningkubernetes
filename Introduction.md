# Kubernetes 
Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

> https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/


#### A Kubernetes cluster consists of the components that represent the control plane and a set of machines called nodes.

When you deploy Kubernetes, you get a cluster.

A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

This document outlines the various components you need to have a complete and working Kubernetes cluster.

> https://kubernetes.io/docs/concepts/overview/components/

### Control Plane Components
The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied).
- kube-apiserver
	- The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.
- etcd 
	- Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
- kube-scheduler
	- Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.
- kube-controller-manager
	- Node controller: Responsible for noticing and responding when nodes go down.
	- Replication controller: Responsible for maintaining the correct number of pods for every replication controller object in the system.
	- Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
	- Service Account & Token controllers: Create default accounts and API access tokens for new namespaces
- cloud-controller-manager
	- Node controller: For checking the cloud provider to determine if a node has been deleted in the cloud after it stops responding
	- Route controller: For setting up routes in the underlying cloud infrastructure
	- Service controller: For creating, updating and deleting cloud provider load balancers

> https://kubernetes.io/docs/concepts/overview/components/#control-plane-components

### Node Coomponents
- kubelet  
	- An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
- kube-proxy
	- kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept. kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.
- Container runtime
	- The container runtime is the software that is responsible for running containers. Kubernetes supports several container runtimes: Docker, containerd, CRI-O, and any implementation of the Kubernetes CRI (Container Runtime Interface).

> https://kubernetes.io/docs/concepts/overview/components/#node-components