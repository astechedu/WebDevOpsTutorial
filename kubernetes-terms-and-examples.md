# Kubernetes Components


[<-- Back](kubernetes.md)

Topics

Kubernetes Terms:

Jobs

[Pods](#pods), [Nodes](#nodes), [Ingress](#ingress), [Services](#services), [Deployment](#deployment), [StatefullSet](#statefullset)

Main Kubernetes Components summarized:

[Volumes](#volumes), [ConfigMap](#configmap), [Sectets](#secrets)

Kubernetes Services: ,Headless,Multi-Port,NodePort,LoadBalancer

[ClusterIP](#clusterip), [Headless](#headless), [Multi-Port](#multi-port), [NodePort](#nodeport), [LoadBalancer](#loadbalancer)





#


# Pods

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

pods/simple-pod.yaml


    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80


To create the Pod shown above, run the following command:

      kubectl apply -f https://k8s.io/examples/pods/simple-pod.yaml


Pod templates:

Controllers for workload resources create Pods from a pod template and manage those Pods on your behalf.

PodTemplates are specifications for creating Pods, and are included in workload resources such as Deployments, Jobs, and DaemonSets.


      apiVersion: batch/v1
      kind: Job
      metadata:
        name: hello
      spec:
        template:
          # This is the pod template
          spec:
            containers:
            - name: hello
              image: busybox:1.28
              command: ['sh', '-c', 'echo "Hello, Kubernetes!" && sleep 3600']
            restartPolicy: OnFailure
          # The pod template ends here






# Nodes

Kubernetes runs your workload by placing containers into Pods to run on Nodes. A node may be a virtual or physical machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods.


The components on a node include the kubelet, a container runtime, and the kube-proxy.


Management

There are two main ways to have Nodes added to the API server:

    1. The kubelet on a node self-registers to the control plane
    2. You (or another human user) manually add a Node object


        {
          "kind": "Node",
          "apiVersion": "v1",
          "metadata": {
            "name": "10.240.79.157",
            "labels": {
              "name": "my-first-k8s-node"
            }
          }
        }





        "conditions": [
          {
            "type": "Ready",
            "status": "True",
            "reason": "KubeletReady",
            "message": "kubelet is posting ready status",
            "lastHeartbeatTime": "2019-06-05T18:38:35Z",
            "lastTransitionTime": "2019-06-05T11:41:27Z"
          }
        ]



Assuming the following custom pod priority classes in a cluster,

        Pod priority class name	Pod priority class value
        custom-class-a	100000
        custom-class-b	10000
        custom-class-c	1000
        regular/unset	0


Within the kubelet configuration the settings for shutdownGracePeriodByPodPriority could look like:

        Pod priority class value	Shutdown period
        100000	10 seconds
        10000	180 seconds
        1000	120 seconds
        0	60 seconds


The corresponding kubelet config YAML configuration would be:

    shutdownGracePeriodByPodPriority:
    
      - priority: 100000
        shutdownGracePeriodSeconds: 10
      - priority: 10000
        shutdownGracePeriodSeconds: 180
      - priority: 1000
        shutdownGracePeriodSeconds: 120
      - priority: 0
        shutdownGracePeriodSeconds: 60



# Services

# Deployment

# Ingress

# Volumes

# ConfigMap

# Secrets

# ClusterIP

# Headless 

# Multi-Port 

# NodePort 

# LoadBalancer

# StatefullSet

# Jobs
