# The Container Ecosystem Project

The ecosystem of awesome new technologies emerging around containers and microservices can be a little overwhelming, to say the least. We thought we might be able to help: welcome to the Container Ecosystem Project. The goals of this project are (1) to clearly lay out the different types technologies that make up the growing container ecosystem and the microservices technology stack – starting from the lowest levels of core container technology, and rising up through layers of abstraction to full-blown container platforms and support tools – and (2) to put forth the latest and greatest examples of each type of technology. This project is a living document – [see below for more info](https://github.com/draios/sysdig-container-ecosystem#about-the-container-ecosystem-project).



## Table of Contents

* The Container Ecosystem
  * [Core Container Technologies](https://github.com/draios/sysdig-container-ecosystem#core-container-technologies)
    * [Container specifications](https://github.com/draios/sysdig-container-ecosystem#container-specifications)
    * [Container runtimes](https://github.com/draios/sysdig-container-ecosystem#container-runtimes)
    * [Container management](https://github.com/draios/sysdig-container-ecosystem#container-management)
    * [Container definition](https://github.com/draios/sysdig-container-ecosystem#container-definition)
    * [Registries](https://github.com/draios/sysdig-container-ecosystem#registries)
    * [Operating systems](https://github.com/draios/sysdig-container-ecosystem#operating-systems)
    * [VM management](https://github.com/draios/sysdig-container-ecosystem#vm-management)
  * [Distributed Container Technologies](https://github.com/draios/sysdig-container-ecosystem#distributed-container-technologies)
    * [Scheduling](https://github.com/draios/sysdig-container-ecosystem#scheduling)
    * [Cluster definition](https://github.com/draios/sysdig-container-ecosystem#cluster-definition)
    * [Service discovery / Distributed configuration storage](https://github.com/draios/sysdig-container-ecosystem#service-discovery--distributed-configuration-storage)
    * [Dynamic configuration management](https://github.com/draios/sysdig-container-ecosystem#dynamic-configuration-management)
  * [Container Platform Technologies](https://github.com/draios/sysdig-container-ecosystem#container-platform-technologies)
    * [Container orchestration platform](https://github.com/draios/sysdig-container-ecosystem#container-orchestration-platform)
    * [Hosted container platform](https://github.com/draios/sysdig-container-ecosystem#hosted-container-platform)
    * [Container platform management](https://github.com/draios/sysdig-container-ecosystem#container-platform-management)
    * [Container-based PaaS](https://github.com/draios/sysdig-container-ecosystem#container-based-paas)
  * [Container-Native Support Technologies](https://github.com/draios/sysdig-container-ecosystem#container-native-support-technologies)
    * [Networking](https://github.com/draios/sysdig-container-ecosystem#networking)
    * [Monitoring / Visibility](https://github.com/draios/sysdig-container-ecosystem#monitoring--visibility)
    * [Data layer](https://github.com/draios/sysdig-container-ecosystem#data-layer)
    * [CI/CD](https://github.com/draios/sysdig-container-ecosystem#cicd)
    * [Security](https://github.com/draios/sysdig-container-ecosystem#security)
    * [Getting started aides](https://github.com/draios/sysdig-container-ecosystem#getting-started-aides)
* [About the Container Ecosystem Project](https://github.com/draios/sysdig-container-ecosystem#about-the-container-ecosystem-project)
* [Further Reading](https://github.com/draios/sysdig-container-ecosystem#further-reading)



## Core Container Technologies

*Use these tools to run a small number of containers on a single host*

#### Container specifications

An abstract definition of a standard "container", allowing an ecosystem of technologies to support a standard container with potentially multiple, interchangeable runtime implementations

* **Docker open source**
  * [Open Container spec](https://github.com/appc/spec): open industry standard for container runtimes; supported by Docker, CoreOS, and most industry leaders; backed by the [Open Container Initiative (OCI)](http://www.opencontainers.org/) (run by the Linux Foundation); currently absorbing CoreOS's AppC standard

* **CoreOS open source**
  * [AppC](https://github.com/appc/spec) (deprecated): CoreOS is now supporting the OCI


#### Container runtimes

This is your actual running container (essentially an abstraction of Linux kernel components like namespaces and cgroups that allow virtualization on top of a shared kernel)

* **Docker open source**
  * [runc](https://github.com/opencontainers/runc): Docker's container runtime, now donated to the OCI as the initial implementation of the standard; essentially a repackaging of libcontainer
  * [libcontainer](https://github.com/opencontainers/runc/tree/master/libcontainer): a Linux container library; enables and abstracts interactions with Linux kernel components to create and control containers

* **CoreOS open source**
  * [rkt](https://github.com/coreos/rkt): CoreOS's container runtime; initially an implementation of the AppC specification, which is now being rolled into the OCI spec

* **Other open source**
  * [LXC](https://linuxcontainers.org/): a Linux container library; originally utilized by runc until release of libcontainer
  * [OpenVZ](https://openvz.org/Main_Page): a Linux container library


#### Container management

These tools abstract low level control of your container runtime adding further functionality and usability

* **Docker open source**
  * [Docker Engine](https://www.docker.com/docker-engine) (aka "Docker"): the core of Docker and its primary interface; creates and runs Docker containers; includes:
    * Docker daemon: runs as a process on the host machine and provides an API that abstracts basic container control functions
    * Docker client: a CLI for interacting with the Docker daemon

* **CoreOS open source**
  * [rkt CLI](https://coreos.com/rkt/docs/latest/commands.html): rkt's container management functionality is delivered on-demand by a binary, rather than a daemon background process

* **Other open source**
  * [LXD](https://linuxcontainers.org/lxd/): daemon and UI for LXC
  * [libvirt](http://libvirt.org/): container and virtualization mgmt library that supports LXC, OpenVZ, and a variety of hypervisor technologies


#### Container definition

These tools allow you to define specific containers, so they can be saved, shared and reproduced

* **Docker open source**
  * [Docker image](https://docs.docker.com/userguide/dockerimages/): a template representing a fully configured container; Docker container runtimes are created from these images; images are created with Dockerfiles and shared over registries
  * [Dockerfile](https://docs.docker.com/articles/dockerfile_best-practices/): text file containing all the commands needed to build a Docker image

* **CoreOS open source**
  * [ACI (App Container Image)](https://github.com/coreos/rkt#rkt-basics): rkt's native container image format (note, rkt also supports Docker images)


#### Registries

Repositories for storing and sharing Docker images

* **Docker open source**
  * [Docker Registry](https://github.com/docker/distribution): open source Docker image registry that can be hosted in your own environment

* **Commercial**
  * Hosted
    * [Docker Hub](https://hub.docker.com/): hosted registry with free paid tiers, private public repositories, and a collection of "official" images
    * [Quay.io](https://quay.io/): CoreOS's hosted registry
  * On-premise
    * [Docker Trusted Registry](https://www.docker.com/docker-trusted-registry)
    * [CoreOS Enterprise Registry](https://coreos.com/products/enterprise-registry)


#### Operating systems

OS's that are designed for hosting containers

* **Docker open source**
  * [boot2docker](http://boot2docker.io/) (basically deprecated by Docker Machine): minimalist Linux for running Docker on PC and Mac in a VM; now used by Docker Machine in certain environments

* **CoreOS open source**
  * [CoreOS](https://coreos.com/): minimalist OS built for running distributed, containerized apps; includes etcd and fleet

* **Other open source**
  * [RancherOS](https://github.com/rancher/os): minimalist, fully containerized OS
  * [Project Atomic](http://www.projectatomic.io/): minimalist Red Hat Linux; versions include RHEL Atomic, CentOS Atomic, and Fedora Atomic
  * [Ubuntu Core "Snappy"](https://developer.ubuntu.com/en/snappy/): minimalist Ubuntu
  * [SmartOS](https://smartos.org/): Solaris-based OS from Joyent that includes [Zones](http://wiki.smartos.org/display/DOC/Zones) (ie. Solaris containers)
  * [Photon OS](https://vmware.github.io/photon/): minimalist OS from VMWare


#### VM management

These tools help you manage the host virtual environments in which you run your containers

* **Docker open source**
  * [Docker Machine](https://github.com/docker/machine): creates and manages host VMs running Docker, including local VMs (eg. VirtualBox) and cloud VMs (eg. Amazon AWS, Google GCP)

* **Other open source**
  * [Hashicorp Vagrant](https://www.vagrantup.com/): creates pre-configured VMs for dev environments based on a variety of "Providers" (virtualization technologies) including Docker containers
  * [Hashicorp Otto](https://www.ottoproject.io/): extends Vagrant to deploy and manage VMs across many platforms


## Distributed Container Technologies

*Use these technologies to run applications on a distributed cluster of containers*

#### Scheduling

These tools manage placement of new containers across abstracted underlying resources

* **Docker open source**
  * [Docker Swarm](https://github.com/docker/swarm/): designed to extend Docker API to a cluster; includes scheduling and service discovery

* **CoreOS open source**
  * [fleet](https://github.com/coreos/fleet): low level orchestration included in CoreOS; supports basic scheduling; can be used to bootstrap Kubernetes for higher level orchestration

* **Other open source**
  * [Chronos](https://github.com/mesos/chronos): framework for scheduling on Mesos


#### Cluster definition

These tools allow you to define and manage a cluster of dependent containers as a single composable entity

* **Docker open source**
  * [Docker Compose](https://github.com/docker/docker/issues/9694): text files used to define and configure a distributed application across a cluster of Docker containers

* **CoreOS open source**
  * [fleet unit file](https://github.com/coreos/fleet/blob/master/Documentation/unit-files-and-scheduling.md): fleet uses a specialized version of systemd unit files to define a distributed application across containers


#### Service discovery / Distributed configuration storage

These tools allow applications within different containers to discover each other and share configuration information (eg. IP addresses or application settings); usually implemented as a globally distributed key-value store

* **Docker open source**
  * Docker Swarm comes with built in service discovery, but can also use etcd, Consul, Zookeeper

* **CoreOS open source**
  * [etcd](https://github.com/coreos/etcd): globally distributed key-value store; included with CoreOS for service discovery

* **Other open source**
  * [Marathon](https://github.com/mesosphere/marathon): framework for initializing long running jobs on Mesos; includes service discovery and cluster management functionality
  * [Hashicorp Consul](https://www.consul.io/): service discovery, key/value store, and cluster health checking; uses [Serf](https://www.serfdom.io/)
  * [Apache ZooKeeper](https://zookeeper.apache.org/): globally distributed key-value store


#### Dynamic configuration management

These tools let you dynamically update application settings based on changes to your distributed key-value store in applications that don't natively support this

* **CoreOS open source**
  * [confd](http://www.confd.io/): originally built for etcd, but now supports Consul and ZooKeeper

* **Other open source**
  * [Consul Template](https://github.com/hashicorp/consul-template): built natively for Consul


## Container Platform Technologies

*Use these technologies as complete platforms for running distributed applications across clusters of containers*

#### Container orchestration platform

These platforms include or abstract away all of the core functionality (listed above) needed for container cluster management ("orchestration"), including container management, scheduling, cluster definition, and service discovery

* **Docker open source**
  * Docker Swarm, Compose, and Machine can all run together to create a complete orchestration platform (still beta); Docker Swarm can also support more advanced orchestration tools like Kubernetes

* **Other open source**
  * [Apache Mesos](http://mesos.apache.org/): mature, highly scalable service that abstracts a pool of underlying resources and distributes "tasks" (including Docker images) from various application frameworks; uses Marathon and Chronos to add cluster management, scheduling, and service discovery; also can support Kubernetes
  * [Kubernetes](http://kubernetes.io/): orchestration platform designed specifically for running microservices on clusters of containers; includes scheduling, cluster management and service discovery through abstractions such as "pods", "replication controllers (RCs)", and "services"; originally from Google, now donated to the [CNCF](https://cncf.io/)
  * [Hashicorp Nomad](https://nomadproject.io/): uses Consul


#### Hosted container platform

These platforms offer container hosting and orchestration as a service

* **Commercial**
  * [Amazon EC2 Container Service (ECS)](https://aws.amazon.com/ecs/)
  * [Google Container Engine](https://cloud.google.com/container-engine/): uses Kubernetes
  * [Tutum](https://www.tutum.co/): still beta
  * [Redhat Openshift](https://enterprise.openshift.com/): uses Kubernetes
  * [Joyent – Triton](https://www.joyent.com/)
  * [Giant Swarm](https://giantswarm.io/): still beta
  * [ProfitBricks](https://www.profitbricks.com/docker): still beta
  * [Modulus](https://modulus.io/)


#### Container platform management

These technologies add further abstracted management and control layers to distributed container environments, often through GUIs

* **Docker open source**
  * [Project Orca](https://youtu.be/BKVKc_xFnw8?list=PLenh213llmcbpJ78mZdh5pnJ_feVT9bezt=5237): opinionated management GUI built on top of full stack of Docker technologies; still alpha

* **Other open source**
  * [Rancher](https://github.com/rancher/rancher): still beta
  * [ContainerShip](https://github.com/containership/containership)
  * [Panamax](http://panamax.io/)
  * [Shipyard](https://github.com/shipyard/shipyard)
  * [Joyent SmartDataCenter](https://github.com/joyent/sdc): uses SmartOS

* **Commercial**
  * [Mesosphere DCOS](https://mesosphere.com/): uses Mesos
  * [CoreOS Tectonic](https://tectonic.com/): uses CoreOS+Kubernetes; still beta
  * [Nirmata](http://nirmata.com/)
  * [ContainerShip Enterprise](http://containership.io/): still beta
  * [StackEngine](http://stackengine.com/)
  * [AppFormix](http://www.appformix.com/)


#### Container-based PaaS

These platforms further abstract container-based infrastructures by managing application code deployment and offering PaaS-like user experiences

* **Other open source**
  * [Deis](https://github.com/deis/deis): container based PaaS; uses CoreOS
  * [Flynn](https://github.com/flynn/flynn): container based PaaS; uses etcd
  * [RedHat Openshift Origin](http://www.openshift.org/)
  * [Cisco Mantl](https://github.com/CiscoCloud/microservices-infrastructure): uses Mesos
  * [Deis Dokku](https://github.com/progrium/dokku): minimalist PaaS


## Container-Native Support Technologies

*Use these additional container-native tools to support your container-based infrastructure*

#### Networking

* **Docker open source**
  * [Docker port expose](https://docs.docker.com/articles/networking/): Docker feature that links a container port to a host port
  * [Docker linking](https://docs.docker.com/userguide/dockerlinks/): Docker feature offering a basic connection between containers on the same host
  * [libnetwork](https://github.com/docker/libnetwork): advanced container networking library (still "under heavy development")

* **CoreOS open source**
  * [flannel](https://github.com/coreos/flannel): overlay network built using etcd that gives each host a separate subnet for its containers

* **Other open source**
  * [Weave](https://github.com/weaveworks/weave): overlay network that puts all containers in a distributed system onto a single virtual network
  * [Calico](http://www.projectcalico.org/): layer 3 virtual network that provides each container with an IP address


#### Monitoring / Visibility

* **Docker open source**
  * Docker ps/top/stats: runtime commands
  * Docker stats API: remote API for streaming basic container metrics; utilized by the Docker Ecosystem Technology Partners for Monitoring

* **Other open source**
  * [sysdig](http://www.sysdig.org/): CLI for deep system/containers visibility; includes curses-based "csysdig" interface
  * [cAdvisor](https://github.com/google/cadvisor): basic container metrics exporter from Google; includes web GUI; [Heapster](https://github.com/kubernetes/heapster) adds Kubernetes support
  * [Weave Scope](https://github.com/weaveworks/scope): container network topologies

* **Commercial**
  * [Sysdig Cloud](https://sysdig.com/): uses sysdig; includes web-based UI, application topologies, and support for all major container formats and orchestration platforms


#### Data layer


* **Other open source**
  * [CusterHQ Flocker](https://clusterhq.com/): data volume manager for running stateful services like databases in containers


#### Log management


* **Docker open source**
  * [Docker logs](https://docs.docker.com/reference/commandline/logs/): runtime command

* **Other open source**
  * [logspout](https://github.com/gliderlabs/logspout): log router for Docker containers


#### CI/CD

* **Commercial**
  * [Shippable](https://app.shippable.com/)
  * [Wercker](http://wercker.com/)


#### Security

* **Commercial**
  * [Twistlock](https://www.twistlock.com/)
  * [Scalock](http://scalock.com/)
  * [Conjur](http://www.conjur.net/)


#### Getting started aides

* **Docker open source**
  * [Docker Kitematic](https://www.docker.com/docker-kitematic): basic Docker GUI designed for getting started with Docker
  * [Docker Toolbox](https://www.docker.com/toolbox): installer for a package of core Docker tools



## About the Container Ecosystem Project

Here at [Sysdig](https://sysdig.com/), the container-native visibility company, we talk to a lot of people in the container ecosystem: both consumers and producers of technology. And wow, there is a LOT of cool technology out there – and so much more coming out all the time. It can be hard to keep up with, even if you're a seasoned expert, much less as a curious newcomer just trying to figure out where to start. There are plenty of great guides out there for various container technologies and use cases (see below for some links). But we had yet to find a clearly organized survey of the different core technologies that make up the container ecosystem and the typical microservices stack. So we decided to make one. Welcome to the Container Ecosystem Project.

The goal of this project is to clearly lay out the different core technologies that might be important for anyone interested in containers and microservices – starting from the lowest levels, and rising up through layers of abstraction to full-blown container platforms. For each type of technology (broken into rows), we've tried to provide a brief description (see the left column), as well as list examples currently available for that technology (see the other columns). We've separated out open source solutions from commercial offerings, and two of the leading open source container technology producers, Docker and CoreOS, each got their own column. Throughout the doc, we've tried to mark beta technologies and parent technologies accordingly. Ideally, this document can introduce you to the microservices stack, and give you some keywords that you can then go research further on your own to learn more – but at least you'll hopefully have the big picture from here.

This framework is not, of course, a perfect science, but we've done our best to create [MECE](https://en.wikipedia.org/wiki/MECE_principle) categories by row, and to put each technology in the most appropriate row. We are almost certainly missing many great technologies, and many technologies listed here do not yet have perfect descriptions. This will be a work in progress. If you have any suggested edits, please [tweet us](https://twitter.com/sysdig) or [send an email](mailto:info@sysdig.com). We'll do our best to keep this document up to date and prune off deprecated or abandoned technologies as the ecosystem evolves.

That's all for now. I hope this can be a useful resource for the community!


## Further Reading

* Docker ecosystem introduction from Digital Ocean: https://www.digitalocean.com/community/tutorial_series/the-docker-ecosystem
* Lists of Docker ecosystem technologies
  * https://www.mindmeister.com/389671722/runc-open-container-ecosystem
  * https://github.com/weihanwang/docker-ecosystem-survey
  * https://github.com/veggiemonk/awesome-docker
* Docker docs: https://docs.docker.com/
* CoreOS docs: https://coreos.com/docs/
