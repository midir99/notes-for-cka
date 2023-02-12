# Kubernetes Overview

## Container v.s. Image

An **image** is a package or a template, it's used to create one or more containers.

**Containers** are running instances of images thatt are isolated and have their own environments and set of processes.

## Container Orchestration

What if the application relies on other containes such as databases or messaging services? Or other backend services? What if the number of users increase and you need to scale your application? How do you scale down when the charge decreases?

To enable this functionalities you need **an underlilying platform with a set of resources and capabilities, the platform needs to orchestrate the connectivity between containers and automatically scale up or down based on the load.**

Automatically deploying and managing containers is known as Container Orchestration.

Some tools to orchestrate:

- Docker Swarm
- Kubernetes
- MESOS

Kubernetes advantages:

- HA.
- Hardware failures do not bring the application down because we have multiple instances of your application running on different nodes.
- User traffic is load balanced accross the various containers.
- When demand increases, deploy more instances of the application seamlessly and within a matter of seconds, we have the ability to do that at service level.
- When we run out of hardware resources scale the number of underlying nodes up or down without having to take down the application.
- All this is done by a set of declarative object configuration files.

**So what is Kubernetes?** It's a container orchestration technology used to orchestrate the deployment and management of hundreds and thousands of containers in a clustered environment.

## Kubernetes architecture

### Node

A node is a machine, physical or virtual on which Kubernetes is installed, a node is a worker machine and that is where containers will be launched by Kubernetes. They were called minions in the past. What if the node on which your application is running fails? The application goes down, so you need more than 1 node.

![](../assets/img/node.png "Nodes")

### Cluster

A cluster is a set of nodes grouped togheter, so if a node fails you have your application still accessible from the other nodes. Moreover having multiple nodes helps sharing the load as well.

![](../assets/img/cluster.png "Cluster")

### Master

Who is reponsible for managing the cluster? Where is the information about members of the cluster stored? How are the nodes monitored? When a node fails, how do you move the workload of the field node to another worker node? There's where the master comes in, the master is another **node** with Kubernetes installed in it and is configured as a master. The master watches over the nodes in the cluster and is responsible for the actual orchestration of containers on the worker nodes.

![](../assets/img/master.png "Master")

### Components

When you install Kubernetes in a system you are actually installing the following components:

- API server  
  The Kubernetes frontend. Users, administration devices, CLIs, everyone talks to the API server to interact with the Kubernetes cluster.

- `etcd` service  
  It's a distributed key-value store used to save all the data its used to mantain the cluster. `etcd` is reponsible of implementing the locks within the cluster to ensure that there are no conflicts between the masters.

- Scheduler  
  Responsible for distributing work on containers across multiple nodes. It locks for newly created containers and assigns them to nodes.

- Controller  
  The controllers are the brain behind orchestration, they are responsible for noticing and responding when nodes, containers or endpoints go down, controllers make decisions to bring up new containers in such cases.

- Container runtime
  The container runtime is the underlying software that is used to run containers, we will be using Docker but there are other options.

- `kubelet` service  
  It is the agent that runs on each node in the cluster.

## Master vs Worker Nodes

We saw two types of servers, **master** and **worker** and a set of components that make up Kubernetes... But how does one server become a master and the other slave? The minion node is where the containers are hosted, to run containers we need a **container runtime** and that is where the container runtime falls. The master server has the kube **API server** and that is what makes it a master. Similarly, the worker nodes have the `kubelet` agent that is reponsible of interacting with the server to provide health information of the worker node and carry out actions requested by the master on the worker nodes. All the information gathered is stored in the key-value store on the master. The master also has the **controller** and the **scheduler**. With this, you can understand what components constitute the master and worker nodes.

![](../assets/img/master-vs-worker.png "Master vs Workers")

## What is `kubectl`?

The `kubectl` tool is used to deploy and manage applications on a Kubernetes cluster, to get cluster information, to get the status of nodes in the cluster, and to manage many other things. Examples:

`kubectl run hello-minikube`  
Command used to deploy applications on the cluster.

`kubectl cluster-info`  
Command used to view information about the cluster.

`kubectl get nodes`  
Command used to list all the nodes part of the cluster.
