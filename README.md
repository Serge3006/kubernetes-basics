# Kubernetes Basics
The following document explain the basics of kubernetes, definitions of some of the most important component, the architecture, typical commands, etc.

# Architecture of Kubernetes
The architecture has two components: The workers nodes or simply nodes and the master nodes. Both can be physical or virtual servers. The master is the main communication interface with the nodes in the architecture.

## Worker Nodes

### Components

Each worker node can run one or more pods. A **Pod** is the smallest component in Kubernetes. It is an abstraction layer that contains the container with the app. For two or more pods to communicate to each other inside a node they can use the IP addresses, however the problem is that if the container dies and is restarted it will have a different IP address. That is where the **Service** component comes into play.

**Service** provides host names that will not change even if pods die and get restarted. Now the communication between pods is made through the Service component.

Another component is the **Ingress** one, which is the interface from external requests. Ingress will route the requests to only the pods that should be exposed, hiding those that should remain secret, such as pods running databases.

The **ConfigMap** is another component that contains the configuration of your application. It could contain information such as the URL of your database.

The **Secret** component stores sensible data such as credentials (username and password).

Volumes allows to store data that should persist if the pods die. The volumes can be local or external to the node.

### Deployments

When working with pods / nodes we don't work directly with them. We work with another abstraction component called **Deployment** where we define the configuration of our nodes / pods.

Deployment is in charge of generating the replicas of our nodes / pods. However, it cannot be used to generate replicas for databases pods.

### Stateful

Basically, it synchonizes databases copies if they are inside the nodes. However, DB's are often hosted outside of K8's clusters, because it is complicated to configure the stateful component.

# Kubectl CRUD commands

Create a deployment
```console
kubectl create deployment nginx-deployment --image=nginx
```

