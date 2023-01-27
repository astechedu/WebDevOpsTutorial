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

[Got To Top](#top)
<a name="pods"></a>
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






[Got To Top](#nodes)
<a name="nodes"></a>
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



        Pod priority class value	Shutdown period
        
        100000	300 seconds
        1000	120 seconds
        0	60 seconds



        memorySwap:
          swapBehavior: LimitedSwap





[Got To Top](#services)
<a name="services"></a>
# Services

An abstract way to expose an application running on a set of Pods as a network service.

With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.

Defining a Service:

A Service in Kubernetes is a REST object, similar to a Pod. 


        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
        spec:
          selector:
            app.kubernetes.io/name: MyApp
          ports:
            - protocol: TCP
              port: 80
              targetPort: 9376





            apiVersion: v1
            kind: Pod
            metadata:
              name: nginx
              labels:
                app.kubernetes.io/name: proxy
            spec:
              containers:
              - name: nginx
                image: nginx:stable
                ports:
                  - containerPort: 80
                    name: http-web-svc

            ---
            apiVersion: v1
            kind: Service
            metadata:
              name: nginx-service
            spec:
              selector:
                app.kubernetes.io/name: proxy
              ports:
              - name: name-of-service-port
                protocol: TCP
                port: 80
                targetPort: http-web-svc



 Services without selectors: 
 
 
        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
        spec:
          ports:
            - protocol: TCP
              port: 80
              targetPort: 9376    




        apiVersion: discovery.k8s.io/v1
        kind: EndpointSlice
        metadata:
          name: my-service-1 # by convention, use the name of the Service
                             # as a prefix for the name of the EndpointSlice
          labels:
            # You should set the "kubernetes.io/service-name" label.
            # Set its value to match the name of the Service
            kubernetes.io/service-name: my-service
        addressType: IPv4
        ports:
          - name: '' # empty because port 9376 is not assigned as a well-known
                     # port (by IANA)
            appProtocol: http
            protocol: TCP
            port: 9376
        endpoints:
          - addresses:
              - "10.4.5.6" # the IP addresses in this list can appear in any order
              - "10.1.2.3"



Multi-Port Services:

        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
        spec:
          selector:
            app.kubernetes.io/name: MyApp
          ports:
            - name: http
              protocol: TCP
              port: 80
              targetPort: 9376
            - name: https
              protocol: TCP
              port: 443
              targetPort: 9377



Environment variables:

        REDIS_PRIMARY_SERVICE_HOST=10.0.0.11
        REDIS_PRIMARY_SERVICE_PORT=6379
        REDIS_PRIMARY_PORT=tcp://10.0.0.11:6379
        REDIS_PRIMARY_PORT_6379_TCP=tcp://10.0.0.11:6379
        REDIS_PRIMARY_PORT_6379_TCP_PROTO=tcp
        REDIS_PRIMARY_PORT_6379_TCP_PORT=6379
        REDIS_PRIMARY_PORT_6379_TCP_ADDR=10.0.0.11



NodePort:

Choosing your own port

        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
        spec:
          type: NodePort
          selector:
            app.kubernetes.io/name: MyApp
          ports:
              # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
            - port: 80
              targetPort: 80
              # Optional field
              # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
              nodePort: 30007



Type LoadBalancer:


        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
        spec:
          selector:
            app.kubernetes.io/name: MyApp
          ports:
            - protocol: TCP
              port: 80
              targetPort: 9376
          clusterIP: 10.0.171.239
          type: LoadBalancer
        status:
          loadBalancer:
            ingress:
            - ip: 192.0.2.127



TLS support on AWS

For partial TLS / SSL support on clusters running on AWS, you can add three annotations to a LoadBalancer service:

        metadata:
          name: my-service
          annotations:
            service.beta.kubernetes.io/aws-load-balancer-ssl-cert: arn:aws:acm:us-east-1:123456789012:certificate/12345678-1234-1234-1234-123456789012



        metadata:
          name: my-service
          annotations:
            service.beta.kubernetes.io/aws-load-balancer-backend-protocol: (https|http|ssl|tcp)




         metadata:
              name: my-service
              annotations:
                service.beta.kubernetes.io/aws-load-balancer-backend-protocol: http
                service.beta.kubernetes.io/aws-load-balancer-ssl-ports: "443,8443"



         metadata:
              name: my-service
              annotations:
                service.beta.kubernetes.io/aws-load-balancer-ssl-negotiation-policy: "ELBSecurityPolicy-TLS-1-2-2017-01"



PROXY protocol support on AWS

To enable PROXY protocol support for clusters running on AWS, you can use the following service annotation:

            metadata:
              name: my-service
              annotations:
                service.beta.kubernetes.io/aws-load-balancer-proxy-protocol: "*"


ELB Access Logs on AWS:


metadata:

      name: my-service
      annotations:
        # Specifies whether access logs are enabled for the load balancer
        service.beta.kubernetes.io/aws-load-balancer-access-log-enabled: "true"

        # The interval for publishing the access logs. You can specify an interval of either 5 or 60 (minutes).
        service.beta.kubernetes.io/aws-load-balancer-access-log-emit-interval: "60"

        # The name of the Amazon S3 bucket where the access logs are stored
        service.beta.kubernetes.io/aws-load-balancer-access-log-s3-bucket-name: "my-bucket"

        # The logical hierarchy you created for your Amazon S3 bucket, for example `my-bucket-prefix/prod`
        service.beta.kubernetes.io/aws-load-balancer-access-log-s3-bucket-prefix: "my-bucket-prefix/prod"
        
  
  
 Connection Draining on AWS:

        metadata:
              name: my-service
              annotations:
                service.beta.kubernetes.io/aws-load-balancer-connection-draining-enabled: "true"
                service.beta.kubernetes.io/aws-load-balancer-connection-draining-timeout: "60"

  

Other ELB annotations

There are other annotations to manage Classic Elastic Load Balancers that are described below.

        metadata:
          name: my-service
          annotations:
            # The time, in seconds, that the connection is allowed to be idle (no data has been sent
            # over the connection) before it is closed by the load balancer
            service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: "60"

            # Specifies whether cross-zone load balancing is enabled for the load balancer
            service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: "true"

            # A comma-separated list of key-value pairs which will be recorded as
            # additional tags in the ELB.
            service.beta.kubernetes.io/aws-load-balancer-additional-resource-tags: "environment=prod,owner=devops"

            # The number of successive successful health checks required for a backend to
            # be considered healthy for traffic. Defaults to 2, must be between 2 and 10
            service.beta.kubernetes.io/aws-load-balancer-healthcheck-healthy-threshold: ""

            # The number of unsuccessful health checks required for a backend to be
            # considered unhealthy for traffic. Defaults to 6, must be between 2 and 10
            service.beta.kubernetes.io/aws-load-balancer-healthcheck-unhealthy-threshold: "3"

            # The approximate interval, in seconds, between health checks of an
            # individual instance. Defaults to 10, must be between 5 and 300
            service.beta.kubernetes.io/aws-load-balancer-healthcheck-interval: "20"

            # The amount of time, in seconds, during which no response means a failed
            # health check. This value must be less than the service.beta.kubernetes.io/aws-load-balancer-healthcheck-interval
            # value. Defaults to 5, must be between 2 and 60
            service.beta.kubernetes.io/aws-load-balancer-healthcheck-timeout: "5"

            # A list of existing security groups to be configured on the ELB created. Unlike the annotation
            # service.beta.kubernetes.io/aws-load-balancer-extra-security-groups, this replaces all other
            # security groups previously assigned to the ELB and also overrides the creation
            # of a uniquely generated security group for this ELB.
            # The first security group ID on this list is used as a source to permit incoming traffic to
            # target worker nodes (service traffic and health checks).
            # If multiple ELBs are configured with the same security group ID, only a single permit line
            # will be added to the worker node security groups, that means if you delete any
            # of those ELBs it will remove the single permit line and block access for all ELBs that shared the same security group ID.
            # This can cause a cross-service outage if not used properly
            service.beta.kubernetes.io/aws-load-balancer-security-groups: "sg-53fae93f"

            # A list of additional security groups to be added to the created ELB, this leaves the uniquely
            # generated security group in place, this ensures that every ELB
            # has a unique security group ID and a matching permit line to allow traffic to the target worker nodes
            # (service traffic and health checks).
            # Security groups defined here can be shared between services.
            service.beta.kubernetes.io/aws-load-balancer-extra-security-groups: "sg-53fae93f,sg-42efd82e"

            # A comma separated list of key-value pairs which are used
            # to select the target nodes for the load balancer
            service.beta.kubernetes.io/aws-load-balancer-target-node-labels: "ingress-gw,gw-name=public-api"




Network Load Balancer support on AWS:

FEATURE STATE: Kubernetes v1.15 [beta]

To use a Network Load Balancer on AWS, use the annotation service.beta.kubernetes.io/aws-load-balancer-type with the value set to nlb.

            metadata:
              name: my-service
              annotations:
                service.beta.kubernetes.io/aws-load-balancer-type: "nlb"




        spec:
          loadBalancerSourceRanges:
            - "143.231.0.0/16"



  Type ExternalName:
  

        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
          namespace: prod
        spec:
          type: ExternalName
          externalName: my.database.example.com
    
    
External IPs:


        apiVersion: v1
        kind: Service
        metadata:
          name: my-service
        spec:
          selector:
            app.kubernetes.io/name: MyApp
          ports:
            - name: http
              protocol: TCP
              port: 80
              targetPort: 9376
          externalIPs:
            - 80.11.12.10






[Got To Top](#top)
<a name="depooyment"></a>
# Deployment

A Deployment provides declarative updates for Pods and ReplicaSets.

You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.


Use Case

The following are typical use cases for Deployments:

    Create a Deployment to rollout a ReplicaSet. The ReplicaSet creates Pods in the background. Check the status of the rollout to see if it succeeds or not.
    Declare the new state of the Pods by updating the PodTemplateSpec of the Deployment. A new ReplicaSet is created and the Deployment manages moving the Pods from the old ReplicaSet to the new one at a controlled rate. Each new ReplicaSet updates the revision of the Deployment.
    Rollback to an earlier Deployment revision if the current state of the Deployment is not stable. Each rollback updates the revision of the Deployment.
    Scale up the Deployment to facilitate more load.
    Pause the rollout of a Deployment to apply multiple fixes to its PodTemplateSpec and then resume it to start a new rollout.
    Use the status of the Deployment as an indicator that a rollout has stuck.
    Clean up older ReplicaSets that you don't need anymore.



Creating a Deployment:

The following is an example of a Deployment. It creates a ReplicaSet to bring up three nginx Pods:



controllers/nginx-deployment.yaml


        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: nginx-deployment
          labels:
            app: nginx
        spec:
          replicas: 3
          selector:
            matchLabels:
              app: nginx
          template:
            metadata:
              labels:
                app: nginx
            spec:
              containers:
              - name: nginx
                image: nginx:1.14.2
                ports:
                - containerPort: 80




        kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml

        kubectl get deployments 



Updating a Deployment

        kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1
        Or
        kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
        kubectl edit deployment/nginx-deployment

        kubectl rollout status deployment/nginx-deployment
        or

        deployment "nginx-deployment" successfully rolled out

        kubectl get rs
        kubectl get pods
        kubectl describe deployments


        kubectl set image deployment/nginx-deployment nginx=nginx:1.161 
        kubectl rollout status deployment/nginx-deployment

        kubectl get rs
        kubectl get pods
        kubectl describe deployment

        kubectl rollout history deployment/nginx-deployment
        kubectl rollout history deployment/nginx-deployment --revision=2

        kubectl rollout undo deployment/nginx-deployment

        or
        kubectl rollout undo deployment/nginx-deployment --to-revision=2
        kubectl get deployment nginx-deployment

        kubectl describe deployment nginx-deployment

        kubectl scale deployment/nginx-deployment --replicas=10
        kubectl autoscale deployment/nginx-deployment --min=10 --max=15 --cpu-percent=80

        kubectl get deploy
        kubectl set image deployment/nginx-deployment nginx=nginx:sometag
        kubectl get rs
        kubectl get deploy
        kubectl get rs
        kubectl get deploy
        kubectl get rs
        kubectl rollout pause deployment/nginx-deployment
        kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
        kubectl rollout history deployment/nginx-deployment
        kubectl get rs
        kubectl set resources deployment/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi
        kubectl rollout resume deployment/nginx-deployment
        kubectl get rs -w

        kubectl get rs
        kubectl rollout status deployment/nginx-deployment

        kubectl patch deployment/nginx-deployment -p '{"spec":{"progressDeadlineSeconds":600}}'
        kubectl describe deployment nginx-deployment
        kubectl rollout status deployment/nginx-deployment





[Got To Top](#top)
<a name="pods"></a>
# Ingress


FEATURE STATE:

An API object that manages external access to the services in a cluster, typically HTTP.

Ingress may provide load balancing, SSL termination and name-based virtual hosting.

Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource.




<img src="https://d33wubrfki0l68.cloudfront.net/91ace4ec5dd0260386e71960638243cf902f8206/c3c52/docs/images/ingress.svg" alt="Image loading...." width="50%">


<img src="https://d33wubrfki0l68.cloudfront.net/36c8934ba20b97859854610063337d2072ea291a/28e8b/docs/images/ingressfanout.svg" alt="Image loading..." width="50%">

service/networking/minimal-ingress.yaml

	apiVersion: networking.k8s.io/v1
	kind: Ingress
	metadata:
	  name: minimal-ingress
	  annotations:
	    nginx.ingress.kubernetes.io/rewrite-target: /
	spec:
	  ingressClassName: nginx-example
	  rules:
	  - http:
	      paths:
	      - path: /testpath
		pathType: Prefix
		backend:
		  service:
		    name: test
		    port:
		      number: 80





service/networking/ingress-resource-backend.yaml 


	apiVersion: networking.k8s.io/v1
	kind: Ingress
	metadata:
	  name: ingress-resource-backend
	spec:
	  defaultBackend:
	    resource:
	      apiGroup: k8s.example.com
	      kind: StorageBucket
	      name: static-assets
	  rules:
	    - http:
		paths:
		  - path: /icons
		    pathType: ImplementationSpecific
		    backend:
		      resource:
		        apiGroup: k8s.example.com
		        kind: StorageBucket
		        name: icon-assets






		kubectl describe ingress ingress-resource-backend





	Examples:
	
	Kind	Path(s)	Request path(s)	Matches?
	Prefix	/	(all paths)	Yes
	Exact	/foo	/foo	Yes
	Exact	/foo	/bar	No
	Exact	/foo	/foo/	No
	Exact	/foo/	/foo	No
	Prefix	/foo	/foo, /foo/	Yes
	Prefix	/foo/	/foo, /foo/	Yes
	Prefix	/aaa/bb	/aaa/bbb	No
	Prefix	/aaa/bbb	/aaa/bbb	Yes
	Prefix	/aaa/bbb/	/aaa/bbb	Yes, ignores trailing slash
	Prefix	/aaa/bbb	/aaa/bbb/	Yes, matches trailing slash
	Prefix	/aaa/bbb	/aaa/bbb/ccc	Yes, matches subpath
	Prefix	/aaa/bbb	/aaa/bbbxyz	No, does not match string prefix
	Prefix	/, /aaa	/aaa/ccc	Yes, matches /aaa prefix
	Prefix	/, /aaa, /aaa/bbb	/aaa/bbb	Yes, matches /aaa/bbb prefix
	Prefix	/, /aaa, /aaa/bbb	/ccc	Yes, matches / prefix
	Prefix	/aaa	/ccc	No, uses default backend
	Mixed	/foo (Prefix), /foo (Exact)	/foo	Yes, prefers Exact






Hostname wildcards:

		   Host	Host header	Match?
		   
		*.foo.com	bar.foo.com	Matches based on shared suffix
		*.foo.com	baz.bar.foo.com	No match, wildcard only covers a single DNS label
		*.foo.com	foo.com	No match, wildcard only covers a single DNS label



service/networking/ingress-wildcard-host.yaml

		apiVersion: networking.k8s.io/v1
		kind: Ingress
		metadata:
		  name: ingress-wildcard-host
		spec:
		  rules:
		  - host: "foo.bar.com"
		    http:
		      paths:
		      - pathType: Prefix
			path: "/bar"
			backend:
			  service:
			    name: service1
			    port:
			      number: 80
		  - host: "*.foo.com"
		    http:
		      paths:
		      - pathType: Prefix
			path: "/foo"
			backend:
			  service:
			    name: service2
			    port:
			      number: 80





service/networking/external-lb.yaml 


		apiVersion: networking.k8s.io/v1
		kind: IngressClass
		metadata:
		  name: external-lb
		spec:
		  controller: example.com/ingress-controller
		  parameters:
		    apiGroup: k8s.example.com
		    kind: IngressParameters
		    name: external-lb







For example:

		---
		apiVersion: networking.k8s.io/v1
		kind: IngressClass
		metadata:
		  name: external-lb-1
		spec:
		  controller: example.com/ingress-controller
		  parameters:
		    # The parameters for this IngressClass are specified in a
		    # ClusterIngressParameter (API group k8s.example.net) named
		    # "external-config-1". This definition tells Kubernetes to
		    # look for a cluster-scoped parameter resource.
		    scope: Cluster
		    apiGroup: k8s.example.net
		    kind: ClusterIngressParameter
		    name: external-config-1







service/networking/default-ingressclass.yaml


		apiVersion: networking.k8s.io/v1
		kind: IngressClass
		metadata:
		  labels:
		    app.kubernetes.io/component: controller
		  name: nginx-example
		  annotations:
		    ingressclass.kubernetes.io/is-default-class: "true"
		spec:
		  controller: k8s.io/ingress-nginx




service/networking/test-ingress.yaml 


		apiVersion: networking.k8s.io/v1
		kind: Ingress
		metadata:
		  name: test-ingress
		spec:
		  defaultBackend:
		    service:
		      name: test
		      port:
			number: 80



kubectl get ingress test-ingress




service/networking/simple-fanout-example.yaml


		apiVersion: networking.k8s.io/v1
		kind: Ingress
		metadata:
		  name: simple-fanout-example
		spec:
		  rules:
		  - host: foo.bar.com
		    http:
		      paths:
		      - path: /foo
			pathType: Prefix
			backend:
			  service:
			    name: service1
			    port:
			      number: 4200
		      - path: /bar
			pathType: Prefix
			backend:
			  service:
			    name: service2
			    port:
			      number: 8080





kubectl describe ingress simple-fanout-example




service/networking/name-virtual-host-ingress.yaml



		apiVersion: networking.k8s.io/v1
		kind: Ingress
		metadata:
		  name: name-virtual-host-ingress
		spec:
		  rules:
		  - host: foo.bar.com
		    http:
		      paths:
		      - pathType: Prefix
			path: "/"
			backend:
			  service:
			    name: service1
			    port:
			      number: 80
		  - host: bar.foo.com
		    http:
		      paths:
		      - pathType: Prefix
			path: "/"
			backend:
			  service:
			    name: service2
			    port:
			      number: 80






service/networking/name-virtual-host-ingress-no-third-host.yaml


		apiVersion: networking.k8s.io/v1
		kind: Ingress
		metadata:
		  name: name-virtual-host-ingress-no-third-host
		spec:
		  rules:
		  - host: first.bar.com
		    http:
		      paths:
		      - pathType: Prefix
			path: "/"
			backend:
			  service:
			    name: service1
			    port:
			      number: 80
		  - host: second.bar.com
		    http:
		      paths:
		      - pathType: Prefix
			path: "/"
			backend:
			  service:
			    name: service2
			    port:
			      number: 80
		  - http:
		      paths:
		      - pathType: Prefix
			path: "/"
			backend:
			  service:
			    name: service3
			    port:
			      number: 80





		apiVersion: v1
		kind: Secret
		metadata:
		  name: testsecret-tls
		  namespace: default
		data:
		  tls.crt: base64 encoded cert
		  tls.key: base64 encoded key
		type: kubernetes.io/tls








service/networking/tls-example-ingress.yaml


		apiVersion: networking.k8s.io/v1
		kind: Ingress
		metadata:
		  name: tls-example-ingress
		spec:
		  tls:
		  - hosts:
		      - https-example.foo.com
		    secretName: testsecret-tls
		  rules:
		  - host: https-example.foo.com
		    http:
		      paths:
		      - path: /
			pathType: Prefix
			backend:
			  service:
			    name: service1
			    port:
			      number: 80




kubectl describe ingress test
kubectl edit ingress test


		spec:
		  rules:
		  - host: foo.bar.com
		    http:
		      paths:
		      - backend:
			  service:
			    name: service1
			    port:
			      number: 80
			path: /foo
			pathType: Prefix
		  - host: bar.baz.com
		    http:
		      paths:
		      - backend:
			  service:
			    name: service2
			    port:
			      number: 80
			path: /foo
			pathType: Prefix
		..





kubectl describe ingress test









[Got To Top](#top)
<a name="pods"></a>
# Volumes







[Got To Top](#top)
<a name="pods"></a>
# ConfigMap


ConfigMaps

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.


ConfigMaps and Pods:

Here's an example ConfigMap that has some keys with single values, and other keys where the value looks like a fragment of a configuration format.


		apiVersion: v1
		kind: ConfigMap
		metadata:
		  name: game-demo
		data:
		  # property-like keys; each key maps to a simple value
		  player_initial_lives: "3"
		  ui_properties_file_name: "user-interface.properties"

		  # file-like keys
		  game.properties: |
		    enemy.types=aliens,monsters
		    player.maximum-lives=5    
		  user-interface.properties: |
		    color.good=purple
		    color.bad=yellow
		    allow.textmode=true    
		   
		      
		      
  configmap/configure-pod.yaml


		apiVersion: v1
		kind: Pod
		metadata:
		  name: configmap-demo-pod
		spec:
		  containers:
		    - name: demo
		      image: alpine
		      command: ["sleep", "3600"]
		      env:
			# Define the environment variable
			- name: PLAYER_INITIAL_LIVES # Notice that the case is different here
				                     # from the key name in the ConfigMap.
			  valueFrom:
			    configMapKeyRef:
			      name: game-demo           # The ConfigMap this value comes from.
			      key: player_initial_lives # The key to fetch.
			- name: UI_PROPERTIES_FILE_NAME
			  valueFrom:
			    configMapKeyRef:
			      name: game-demo
			      key: ui_properties_file_name
		      volumeMounts:
		      - name: config
			mountPath: "/config"
			readOnly: true
		  volumes:
		  # You set volumes at the Pod level, then mount them into containers inside that Pod
		  - name: config
		    configMap:
		      # Provide the name of the ConfigMap you want to mount.
		      name: game-demo
		      # An array of keys from the ConfigMap to create as files
		      items:
		      - key: "game.properties"
			path: "game.properties"
		      - key: "user-interface.properties"
			path: "user-interface.properties"
			    
      
      
 
 
 
 
 This is an example of a Pod that mounts a ConfigMap in a volume:



		apiVersion: v1
		kind: Pod
		metadata:
		  name: mypod
		spec:
		  containers:
		  - name: mypod
		    image: redis
		    volumeMounts:
		    - name: foo
		      mountPath: "/etc/foo"
		      readOnly: true
		  volumes:
		  - name: foo
		    configMap:
		      name: myconfigmap

 
 
 
 
Immutable ConfigMaps:        
     
        
		apiVersion: v1
		kind: ConfigMap
		metadata:
		  ...
		data:
		  ...
		immutable: true 
			












[Got To Top](#top)
<a name="pods"></a>
# Secrets




[Got To Top](#top)
<a name="pods"></a>
# ClusterIP



[Got To Top](#top)
<a name="pods"></a>
# Headless 



[Got To Top](#top)
<a name="pods"></a>
# Multi-Port 




[Got To Top](#top)
<a name="pods"></a>
# NodePort 




[Got To Top](#top)
<a name="pods"></a>
# LoadBalancer




[Got To Top](#top)
<a name="pods"></a>
# StatefullSet

StatefulSet is the workload API object used to manage stateful applications.

Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.


Using StatefulSets

StatefulSets are valuable for applications that require one or more of the following.

    Stable, unique network identifiers.
    Stable, persistent storage.
    Ordered, graceful deployment and scaling.
    Ordered, automated rolling updates.
    
    


Components:

The example below demonstrates the components of a StatefulSet.


		apiVersion: v1
		kind: Service
		metadata:
		  name: nginx
		  labels:
		    app: nginx
		spec:
		  ports:
		  - port: 80
		    name: web
		  clusterIP: None
		  selector:
		    app: nginx
		---
		apiVersion: apps/v1
		kind: StatefulSet
		metadata:
		  name: web
		spec:
		  selector:
		    matchLabels:
		      app: nginx # has to match .spec.template.metadata.labels
		  serviceName: "nginx"
		  replicas: 3 # by default is 1
		  minReadySeconds: 10 # by default is 0
		  template:
		    metadata:
		      labels:
			app: nginx # has to match .spec.selector.matchLabels
		    spec:
		      terminationGracePeriodSeconds: 10
		      containers:
		      - name: nginx
			image: registry.k8s.io/nginx-slim:0.8
			ports:
			- containerPort: 80
			  name: web
			volumeMounts:
			- name: www
			  mountPath: /usr/share/nginx/html
		  volumeClaimTemplates:
		  - metadata:
		      name: www
		    spec:
		      accessModes: [ "ReadWriteOnce" ]
		      storageClassName: "my-storage-class"
		      resources:
			requests:
			  storage: 1Gi
    







		apiVersion: apps/v1
		kind: StatefulSet
		...
		spec:
		  persistentVolumeClaimRetentionPolicy:
		    whenDeleted: Retain
		    whenScaled: Delete
		...




[Got To Top](#top)
<a name="pods"></a>
# Jobs
