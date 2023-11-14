<h1> Kubernetes </h1>

<h3> Introduction </h3>

---


Kubernetes is usually defined as a container orchestration platform.

Now before proceeding lets understand what is container, docker and how it differs from kubernetes.

***Containers*** : Containers are light weight packages of software which contain all the dependecies required to run that software in any env.

- Containers are light weight as compared to VM, as each VM has a full OS but in case of container they share a base OS image and uses resources from the host OS.
- Docker is a container platform which enables user with his container journey. There are other platform as well like podman but docker is mostly used across all the orgarnisation. 
  
***Differnce between Docker and Kubernetes***

- The lowest level of deployment in Docker is container, i.e. once the docker file is built an image is created. using that image we can run a container (which is nothing but the instance of software which user wants to run).
- The lowest level of deployment in Kubernetes is POD. POD is just a wrapper around containers. 
- Generally kubernetes is used in PROD  env and not Docker because of the following reasons.
  - __Host__: Docker runs on single host, so if there is any issue identified in that host the applciation will be affected. While Kubernetes runs on a cluster (which consists of 1 or more master and worker node).
  - __AutoScaling__: Kubernetes provides some advance features by which user can spin up new Pods based on the traffic, this is missing in Docker.
  - __AutoHealing__: Kubernetes contains components which constantly monitor the health of the POD and if any POD has issue , kubernetes component identifies it and it helps by creating new POD before the old POD is down.
  - __Enterprise level support__: There are many advanced concepts like loadbalancing, security etc. which are supported in Kubernetes and are not there in docker.

**___Kubernetes architecture:___**
- Kubernetes is clustered architecture which contains 1 or more master node and worked node..
- Each master and worked node has multiple components by which Kubernetes provide the features for container orchestration.

- ***Worker Node/Data Plane:*** 
  - worker node consists of below components:
    - __Kubelet__: Kubelet is a process which will make sure that all the PODs are always running and if it encouters some issue in POD it informs the same to apiserver in master node.
    - __Kubeproxy__: it provides networking, ip address - which basically provides the IP address to all the pods which are running and default load balancing inside kubernetes.
    - __Container runtime__ : For a container to run inside kubernetes it needs container runtime..dockershim is container runtime provided by docker, containerD , crio etc. are some other example of container runtime which are used in kubernetes.

- ***Master Node/Control Plane:***
  - Master Node consists of below components:
    - __apiserver__: It exposes kubernetes to external world. example if user is deciding to create a POD, the request would come to apiserver first..apiserver will decide on which node the pod will be scheduled and it will call scheduler
    - __scheduler__: once apiserver will send the signal scheduler will make sure to create that POD in the respective node. scheduler is responsible for scheduling the resource in kubernetes.
    - __etcd__: it contains the entire cluster information in key value store. it is used to create backup of the cluster.
    - __controller manager__: kubernetes support autoscalling, to support that kubernetes has controller like replicaset. so if user request 2 instance of the POD replicaset controller will make sure that it will bring 2 POD UP.
      - So to summarise controller manager make sure that controller like replicaset are always UP.
    - __cloud controller manager (CCM)__: when kubernetes is running on cloud platform (EKS/AKS), so when user request to create a resource such as LB/storage service on cloud platform than kubernetes has to provide the input from user to cloud provider understandable format. 
      - Kubernetes provides CCM which is an open source utility where cloud providers which want to run kubernetes will write its logic. 

**Difference between POD and container**:
- POD is a wrapper created on top of container. POD can contain 1 or multiple container (called as sidecar).
- The benefit of using multiple container in a POD is they will have shared networking and sidecar container will be able to access the main container directly.
- cluster IP address is assigned at the POD level by Kubeproxy and not container level.


- Deployment --> Replicaset --> POD (container, sidecar)



Service:
1. Load balancing: it balances the incoming request and decide to send it to correct POD
2. Service discovery: when a new pod is UP it discovers that using the label and selectors (as new POD will have different IP) and redirect the traffic to that new POD.
3. Expose to the outside world:Service can allow you to expose your application to the outside world, below is how it does.
      Service Type
        --> ClusterIP : Application can be accessed inside the cluster. only 1 and 2 are possible.
        -->Node Port : Application can be accessed inside your org (intranet) whoever has access to your node.
         --> Load balancing: applications can be accessed from the external world.
