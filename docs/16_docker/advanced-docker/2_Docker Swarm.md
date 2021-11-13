---
layout: default
title: 2_Docker Swarm
parent: docker.md
# nav_order: 1
permalink: /docker/swarm
---
<div align="center" markdown="1">
Docker  / Java resources / Tutorial

{: .fs-8 .fw-400 }
</div>

Swarm as a secure cluster#
On the clustering front, Swarm groups one or more Docker nodes and lets you manage them as a cluster. Out-of-the-box, you get an encrypted distributed cluster store, encrypted networks, mutual TLS, secure cluster join tokens, and a PKI that makes managing and rotating certificates a breeze. You can even non-disruptively add and remove nodes. It’s a beautiful thing.

While we cover some aspects of Swarm security in this chapter, we go a lot deeper in a later chapter.


Swarm as an orchestrator#
On the orchestration front, Swarm exposes a rich API that allows you to deploy and manage complex microservices apps with ease. You can define your apps in declarative manifest files and deploy them to the Swarm with native Docker commands. You can even perform rolling updates, rollbacks, and scaling operations. Again, all with simple commands.

Swarm vs. Kubernetes#
Docker Swarm competes directly with Kubernetes — they both orchestrate containerized applications. While it’s true that Kubernetes has more momentum and a more active community and ecosystem, Docker Swarm is an excellent technology and a lot easier to configure and deploy. It’s a great option for small-to-medium businesses and application deployments.

Swarm nodes#
On the clustering front, a swarm consists of one or more Docker nodes. These can be physical servers, VMs, Raspberry Pi’s, or cloud instances. The only requirement is that all nodes have Docker installed and can communicate over reliable networks.

Managers and workers#
Nodes are configured as managers or workers. Managers look after the cluster’s control plane, meaning things like the state of the cluster and dispatching tasks to workers. Workers accept tasks from managers and execute them.

Swarm configuration#
The configuration and state of the swarm is held in a distributed etcd database located on all managers. It’s kept in memory and is extremely up-to-date. But the best thing about it is that it requires zero configuration; it’s installed as part of the swarm and takes care of itself.

Swarm security#
Something game-changing on the clustering front is the approach to security. TLS is so tightly integrated that it’s impossible to build a swarm without it. In today’s security-conscious world, things like this deserve all the plaudits they get. Swarm uses TLS to encrypt communications, authenticate nodes, and authorize roles. Automatic key rotation is also thrown in as the icing on the cake. And the best part is that it all happens so smoothly that you don’t even know it’s there.

Orchestration#
The atomic unit of scheduling on a swarm is the service on the application orchestration front. This is a new object in the API, introduced along with swarm, and is a higher-level construct that wraps some advanced features around containers. These include scaling, rolling updates, and simple rollbacks. It’s useful to think of a service as an enhanced container.