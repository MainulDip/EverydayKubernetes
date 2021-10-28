# Overview
Start by
```sh
git clone https://github.com/MainulDip/EverydayKubernetes.git
```
___

This is a list and lite documentation of everyday use Kubernetes commands :)

## Kubernetes Brif:
=> Container orchestration tool to manage multiple containers (100 to 1000 containers), ie docker containers
=> Offer no downtime with high performance and scalability for apps, also offer disaster recovery (backup and restores)

## Kubernetes Basic Architecture: 
=> One master node and multiple worker nodes
=> Containers (docker containers) are deployed through Worker nodes.
=> Master node manages Kubernetes processess (like api servers), Controller manager, Scheduler and "etcd" key/value storage (hold state of the kubernetes clusters, snapshots) and also virtual network

=> Virtual Network creates one unified machine
=> Worker nodes take most of the loads as they run the app/s and tons of containers. Thus they need more resources
=> Master node need less resources. But loosing control over master node makes everything unaccessable.
=> In production Env, at least 2 master  for backup. If one master is down, the cluster remain running by other master node.

## Kubernetes Components
=> Pod is the Smallest Unit of Kubernetes Worker node. It is the abstraction over containers
=> Usually 1 application per pod
=> Each pod gets its own ip address (internal dynamic ip, changes every time new pod is assaigned )
=> Pod can die easily (pod funarel), for that reason service (static ip) is used.
=> Service provide permanent (static) IP address. Lifecycle of Pod and Service is not connected
=> External (public) and Internal (private)
=> Ingress Component. Instade of service, request goes to Ingress first. Ingress decides to response with Public/Private services


## Config Map and Secret for password/credentials storage
=> External Config of the app. It helps to cnofiguire the running images on the fly. Bypass the nececity of building the image again on config change. Like Database URL changes, etc.

=> Secret store data in base64 format. Can use it as environment variables or as a properties file.

## Volumes and data storage:
=> Volumes Resolve data loss on app crashes or pod/services restarts. Keep persistance. Volume can be local/remote(cloud) storage both inside and outside of the Kubernetes clusters.
=> Kubernetes doesn't manage data persistance. You have to configure.

## Deployment Statefull Sets:
=> Service serves with permanent IP and as load balancers
=> Define blueprint for pods. So that a new pod can be created if app crashes.
=> In practice, DevOps will not create pods but Deployments. On Deoloyment, you will specify about the reolicas and scalability.
=> Deployments are abatraction of pods. In Practice you will mostly work with Deployments, not pods.

=> Database (state) replication is done by StatefulSet (not by deployments). So databases should be created by StatefulSet. For state-less app, deployments can be used. Statefulset (like deployment) will takecare of replicating pods (is chashed), scale up or down and make sure of database syncronization and resolve inconsistant read and write to the database.

=> Databases are often hosted outside of the Kubuernetes clusters because configuring Statefulset is tidious and complex.

## Summary of the main Kubernetes Components
=>  Pod (abstraction of containers)
    Service (communication between pods)
    Ingress (route traffic into cluster)


=>  ConfigMap (external configuration)
    Secrets (external configuration)

=> Volumes (Data persistance)

=>  Deployment (Pod blueprint and replicating Mechanism)
    Statefulset (Pod blueprint and replicating Mechanism)

## MiniKube and KubeCTL

=> Minikube (One Node Cluster): Test on local machine. On this, Master and Node processes run on One machine. Docker Container Runtime is pre-installed.
=> KubeCTL: A command-line tool/client for interacting with kubernetes cluster. It can interact with Api Server of the Master processes.

## Installing Minikube and Kubectl:
=> Follow officia operating system specific instructions 


### Minikube and Kubectl walkthrough:

```sh
minikube start --driver=docker
```
Error: Exiting due to PROVIDER_DOCKER_NEWGRP

```sh
docker system prune
minikube delete

minikube start --driver=docker

minikube start --force --driver=docker

sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
Error: Got permission denied while trying to connect to the Docker daemon socket code

Solved: From https://docs.docker.com/engine/install/linux-postinstall/ create a Unix group called docker and add user

```sh
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```


### Minikube Startup and verify working Commands:
=> Set --driver=docker to minikube when starting and make as default
```sh
minikube start --driver=docker
minikube config set driver docker
```
=> Test if minikube working (will print Client and Server version)
```sh
kubectl version
kubectl get nodes
minikube status
```

### Basic Kubectl Commands:


Note: Deep dive into "Kubernetes Architecture" to know more about how "Master and Worker Node actually and the processes"

#### Happy Coding :) 