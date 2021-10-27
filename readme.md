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

#### Happy Coding :) 