# Kubernetes Glossary




Affinity

In Kubernetes, affinity is a set of rules that give hints to the scheduler about where to place pods.[+]

Annotation

A key-value pair that is used to attach arbitrary non-identifying metadata to objects.[+]

API Group

A set of related paths in Kubernetes API.[+]

API server

Also known as:kube-apiserver

The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.[+]
Applications
The layer where various containerized applications run. [+]
cgroup (control group)

A group of Linux processes with optional resource isolation, accounting and limits.[+]

Cluster

A set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.[+]

Container

A lightweight and portable executable image that contains software and all of its dependencies.[+]
Container Environment Variables

Container environment variables are name=value pairs that provide useful information into containers running in a pod[+]
Container Runtime

The container runtime is the software that is responsible for running containers.[+]
Container runtime interface (CRI)

The container runtime interface (CRI) is an API for container runtimes to integrate with kubelet on a node.[+]
Control Plane

The container orchestration layer that exposes the API and interfaces to define, deploy, and manage the lifecycle of containers.[+]
Controller

In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state.[+]
CustomResourceDefinition

Custom code that defines a resource to add to your Kubernetes API server without building a complete custom server.[+]
DaemonSet

Ensures a copy of a Pod is running across a set of nodes in a cluster.[+]
Data Plane
The layer that provides capacity such as CPU, memory, network, and storage so that the containers can run and connect to a network. [+]
Deployment

An API object that manages a replicated application, typically by running Pods with no local state.[+]
Device Plugin

Device plugins run on worker Nodes and provide Pods with access to resources, such as local hardware, that require vendor-specific initialization or setup steps.[+]
Disruption

Disruptions are events that lead to one or more Pods going out of service. A disruption has consequences for workload resources, such as Deployment, that rely on the affected Pods.[+]
Docker

Docker (specifically, Docker Engine) is a software technology providing operating-system-level virtualization also known as containers.[+]
Dockershim

The dockershim is a component of Kubernetes version 1.23 and earlier. It allows the kubelet to communicate with Docker Engine.[+]
Ephemeral Container

A Container type that you can temporarily run inside a Pod.[+]
Event

Each Event is a report of an event somewhere in the cluster. It generally denotes some state change in the system.[+]
Extensions

Extensions are software components that extend and deeply integrate with Kubernetes to support new types of hardware.[+]
Feature gate

Feature gates are a set of keys (opaque string values) that you can use to control which Kubernetes features are enabled in your cluster.[+]
Finalizer

Finalizers are namespaced keys that tell Kubernetes to wait until specific conditions are met before it fully deletes resources marked for deletion. Finalizers alert controllers to clean up resources the deleted object owned.[+]
Garbage Collection

Garbage collection is a collective term for the various mechanisms Kubernetes uses to clean up cluster resources.[+]
Image

Stored instance of a Container that holds a set of software needed to run an application.[+]
Init Container

One or more initialization containers that must run to completion before any app containers run.[+]
Job

A finite or batch task that runs to completion.[+]
kube-controller-manager

Control plane component that runs controller processes.[+]
kube-proxy

kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.[+]
Kubectl
Also known as:kubectl

Command line tool for communicating with a Kubernetes cluster's control plane, using the Kubernetes API.[+]
Kubelet

An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.[+]
Kubernetes API

The application that serves Kubernetes functionality through a RESTful interface and stores the state of the cluster.[+]
Label

Tags objects with identifying attributes that are meaningful and relevant to users.[+]
LimitRange

Provides constraints to limit resource consumption per Containers or Pods in a namespace.[+]
Logging

Logs are the list of events that are logged by cluster or application.[+]
Manifest

Specification of a Kubernetes API object in JSON or YAML format.[+]
Master

Legacy term, used as synonym for nodes hosting the control plane.[+]
Minikube

A tool for running Kubernetes locally.[+]
Mirror Pod

A pod object that a kubelet uses to represent a static pod[+]
Name

A client-provided string that refers to an object in a resource URL, such as /api/v1/pods/some-name.[+]
Namespace

An abstraction used by Kubernetes to support isolation of groups of resources within a single cluster.[+]
Node

A node is a worker machine in Kubernetes.[+]
Object

An entity in the Kubernetes system. The Kubernetes API uses these entities to represent the state of your cluster.[+]
Pod

The smallest and simplest Kubernetes object. A Pod represents a set of running containers on your cluster.[+]
Pod Lifecycle

The sequence of states through which a Pod passes during its lifetime.[+]
Pod Security Policy

Enables fine-grained authorization of Pod creation and updates.[+]
QoS Class

QoS Class (Quality of Service Class) provides a way for Kubernetes to classify Pods within the cluster into several classes and make decisions about scheduling and eviction.[+]
RBAC (Role-Based Access Control)

Manages authorization decisions, allowing admins to dynamically configure access policies through the Kubernetes API.[+]
ReplicaSet

A ReplicaSet (aims to) maintain a set of replica Pods running at any given time.[+]
Resource Quotas

Provides constraints that limit aggregate resource consumption per Namespace.[+]
Selector

Allows users to filter a list of resources based on labels.[+]
Service

An abstract way to expose an application running on a set of Pods as a network service.[+]
ServiceAccount

Provides an identity for processes that run in a Pod.[+]
Shuffle-sharding

A techni

    que for assigning requests to queues that provides better isolation than hashing modulo the number of queues.[+]
    StatefulSet

    Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.[+]
    Static Pod

    A pod managed directly by the kubelet daemon on a specific node,[+]
    Taint

    A core object consisting of three required properties: key, value, and effect. Taints prevent the scheduling of Pods on nodes or node groups.[+]
    Toleration

    A core object consisting of three required properties: key, value, and effect. Tolerations enable the scheduling of pods on nodes or node groups that have matching taints.[+]
    UID

    A Kubernetes systems-generated string to uniquely identify objects.[+]
    Volume

    A directory containing data, accessible to the containers in a Pod.[+]
    Workload

    A workload is an application running on Kubernetes.[+]

Feedback

Was this page helpful?
