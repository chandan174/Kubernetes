<h1> Kubernetes </h1>

<h3> Introduction </h3>

---


Kubernetes is usually defined as a container orchestration platform.

Now before proceeding lets understand what is container, docker and how it differs from kubernetes.

***Containers*** : Containers are light weight packages of software which contain all the dependecies required to run that software in any env.

- Containers are light weight as compared to VM, as each VM has a full OS but in case of container they share a base OS image and uses resources from the host OS.
- Docker is a container platform which enables user with his container journey. There are other platform as well like podman but docker is mostly used across all the orgarnisation. 
  
***Differnce between docker and kubernetes***

- The basic unit in Docker is container, i.e. once the docker file is built an image is created. using that image we can run a container (which is nothing but the instance of software which user wants to run).
- The basic unit of Kubernetes is POD. POD is just a wrapper around containers. 
- Generally kubernetes is used in PROD  env and not Docker because of the following reasons.
  - __Host__: Docker runs on single host, so if there is any issue identified in that host the applciation will be affected. While Kubernetes runs on a cluster (which consists of 1 or more master and worker node).
  - __AutoScaling__: Kubernetes provides some advance features by which user can spin up new Pods based on the traffic, this is missing in Docker.
  - __AutoHealing__: Kubernetes contains components which constantly monitor the health of the POD and if any POD has issue , kubernetes component identifies it and it helps by creating new POD before the old POD is down.
  - __Enterprise level support__: There are many advanced concepts like loadbalancing, security etc. which are supported in Kubernetes and are not there in docker.


    
