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
