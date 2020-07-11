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
- kube-apiserver
- etcd 
- kube-scheduler
- kube-controller-manager
- cloud-controller-manager

> https://kubernetes.io/docs/concepts/overview/components/#control-plane-components

### Node Coomponents
- kubelet  
- kube-proxy
- Container runtime