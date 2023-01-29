# Kubernetes Components


[<-- Back](kubernetes.md)

Topics

Kubernetes Terms:

Jobs

[Pods](#pods), [Nodes](#nodes), [Ingress](#ingress), [Services](#services), [Deployment](#deployment), [StatefullSet](#statefullset)

Main Kubernetes Components summarized:

[Volumes](#volumes), [ConfigMap](#configmap), [Sectets](#secrets)

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






[Got To Top](#top)
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





[Got To Top](#top)
<a name="services"></a>
# Services


service-deployment.yml:



	apiVersion: v1
	kink: Service
	metadata:
	  name: demoservice
	spec: 
	 ports: 
	  - port: 80
	    targetPort: 80
	 selector:
	   name: deployment
	 type: ClusterIP




   kubectl apply -f service-deployment.yml
   kubectl get po -o wide




#
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


deployhttpd.yml: 


	apiVersion: v1
	kind: Deployment
	metadata:
	  name: mydeployment
	spec:
	  replicas: 1
	  selector:
	   matchLabels:
	     name: deployment
	  template:
	    metadata:
	      name: testpod1
	      labels:
		name: deployment
	    spec:
	     containers: 
	       - name: c00
		 image: httpd
		 ports:
		 - containerPort: 80



     kubectl apply -f deployhttpd.yml
     kubectl get deployment

#
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
<a name="volumes"></a>
# Volumes


volumes-hostpath.yml (Tested Code)


	apiVersion: v1
	kind: Pod
	metadata:
	  name: myvolhostpath
	spec:
	  containers:
	  - name: testc
	    image: centos
	    command: ["/bin/bash", "-c", "sleep 15000"]
	    volumeMounts:
	     - name: testvolume
	       mountPath: /tmp/hostpath               
	  volumes:
	  - name: testvolume
	    hostPath: 
	      path: /tmp/data 



    kubectl apply -f volumes-hostpath.yml
    kubectl get po
    
#

Volumes:

On-disk files in a container are ephemeral, which presents some problems for non-trivial applications when running in containers. One problem is the loss of files when a container crashes. The kubelet restarts the container but with a clean state. A second problem occurs when sharing files between containers running together in a Pod. The Kubernetes volume abstraction solves both of these problems. Familiarity with Pods is suggested.
Background

Creating an AWS EBS volume

Before you can use an EBS volume with a pod, you need to create it.

aws ec2 create-volume --availability-zone=eu-west-1a --size=10 --volume-type=gp2

Make sure the zone matches the zone you brought up your cluster in. Check that the size and EBS volume type are suitable for your use.
AWS EBS configuration example

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-ebs
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-container
		    volumeMounts:
		    - mountPath: /test-ebs
		      name: test-volume
		  volumes:
		  - name: test-volume
		    # This AWS EBS volume must already exist.
		    awsElasticBlockStore:
		      volumeID: "<volume id>"
		      fsType: ext4

If the EBS volume is partitioned, you can supply the optional field partition: "<partition number>" to specify which partition to mount on.
AWS EBS CSI migration
FEATURE STATE: Kubernetes v1.25 [stable]

The cinder volume type is used to mount the OpenStack Cinder volume into your pod.
Cinder volume configuration example

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-cinder
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-cinder-container
		    volumeMounts:
		    - mountPath: /test-cinder
		      name: test-volume
		  volumes:
		  - name: test-volume
		    # This OpenStack volume must already exist.
		    cinder:
		      volumeID: "<volume id>"
		      fsType: ext4

OpenStack CSI migration
FEATURE STATE: Kubernetes v1.24 [stable]

The CSIMigration feature for Cinder is enabled by default since Kubernetes 1.21. It redirects all plugin operations from the existing in-tree plugin to the cinder.csi.openstack.org Container Storage Interface (CSI) Driver. OpenStack Cinder CSI Driver must be installed on the cluster.

When referencing a ConfigMap, you provide the name of the ConfigMap in the volume. You can customize the path to use for a specific entry in the ConfigMap. The following configuration shows how to mount the log-config ConfigMap onto a Pod called configmap-pod:

		apiVersion: v1
		kind: Pod
		metadata:
		  name: configmap-pod
		spec:
		  containers:
		    - name: test
		      image: busybox:1.28
		      volumeMounts:
			- name: config-vol
			  mountPath: /etc/config
		  volumes:
		    - name: config-vol
		      configMap:
			name: log-config
			items:
			  - key: log_level
			    path: log_level

The log-config ConfigMap is mounted as a volume, and all contents stored in its log_level entry are mounted into the Pod at path /etc/config/log_level. Note that this path is derived from the volume's mountPath and the path keyed with log_level.
Note:

    You must create a ConfigMap before you can use it.

    A container using a ConfigMap as a subPath volume mount will not receive ConfigMap updates.

    Text data is exposed as files using the UTF-8 character encoding. For other character encodings, use binaryData.


A size limit can be specified for the default medium, which limits the capacity of the emptyDir volume. The storage is allocated from node ephemeral storage. If that is filled up from another source (for example, log files or image overlays), the emptyDir may run out of capacity before this limit.
Note: If the SizeMemoryBackedVolumes feature gate is enabled, you can specify a size for memory backed volumes. If no size is specified, memory backed volumes are sized to 50% of the memory on a Linux host.
emptyDir configuration example

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-pd
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-container
		    volumeMounts:
		    - mountPath: /cache
		      name: cache-volume
		  volumes:
		  - name: cache-volume
		    emptyDir:
		      sizeLimit: 500Mi

fc (fibre channel)

An fc volume type allows an existing fibre channel block storage volume to mount in a Pod. You can specify single or multiple target world wide names (WWNs) using the parameter targetWWNs in your Volume configuration. If multiple WWNs are specified, targetWWNs expect that those WWNs are from multi-path connections.
Note: You must configure FC SAN Zoning to allocate and mask those LUNs (volumes) to the target WWNs beforehand so that Kubernetes hosts can access them.

Creating a GCE persistent disk

Before you can use a GCE persistent disk with a Pod, you need to create it.

gcloud compute disks create --size=500GB --zone=us-central1-a my-data-disk

GCE persistent disk configuration example

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-pd
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-container
		    volumeMounts:
		    - mountPath: /test-pd
		      name: test-volume
		  volumes:
		  - name: test-volume
		    # This GCE PD must already exist.
		    gcePersistentDisk:
		      pdName: my-data-disk
		      fsType: ext4

Regional persistent disks

The Regional persistent disks feature allows the creation of persistent disks that are available in two zones within the same region. In order to use this feature, the volume must be provisioned as a PersistentVolume; referencing the volume directly from a pod is not supported.
Manually provisioning a Regional PD PersistentVolume


gcloud compute disks create --size=500GB my-data-disk
  --region us-central1
  --replica-zones us-central1-a,us-central1-b

Regional persistent disk configuration example

		apiVersion: v1
		kind: PersistentVolume
		metadata:
		  name: test-volume
		spec:
		  capacity:
		    storage: 400Gi
		  accessModes:
		  - ReadWriteOnce
		  gcePersistentDisk:
		    pdName: my-data-disk
		    fsType: ext4
		  nodeAffinity:
		    required:
		      nodeSelectorTerms:
		      - matchExpressions:
			# failure-domain.beta.kubernetes.io/zone should be used prior to 1.21
			- key: topology.kubernetes.io/zone
			  operator: In
			  values:
			  - us-central1-a
			  - us-central1-b

Here is an example of a gitRepo volume:

		apiVersion: v1
		kind: Pod
		metadata:
		  name: server
		spec:
		  containers:
		  - image: nginx
		    name: nginx
		    volumeMounts:
		    - mountPath: /mypath
		      name: git-volume
		  volumes:
		  - name: git-volume
		    gitRepo:
		      repository: "git@somewhere:me/my-git-repository.git"
		      revision: "22f1d8406d464b0c0874075539c1f2e96c253775"


hostPath configuration example

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-pd
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-container
		    volumeMounts:
		    - mountPath: /test-pd
		      name: test-volume
		  volumes:
		  - name: test-volume
		    hostPath:
		      # directory location on host
		      path: /data
		      # this field is optional
		      type: Directory

Caution: The FileOrCreate mode does not create the parent directory of the file. If the parent directory of the mounted file does not exist, the pod fails to start. To ensure that this mode works, you can try to mount directories and files separately, as shown in the FileOrCreateconfiguration.
hostPath FileOrCreate configuration example

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-webserver
		spec:
		  containers:
		  - name: test-webserver
		    image: registry.k8s.io/test-webserver:latest
		    volumeMounts:
		    - mountPath: /var/local/aaa
		      name: mydir
		    - mountPath: /var/local/aaa/1.txt
		      name: myfile
		  volumes:
		  - name: mydir
		    hostPath:
		      # Ensure the file directory is created.
		      path: /var/local/aaa
		      type: DirectoryOrCreate
		  - name: myfile
		    hostPath:
		      path: /var/local/aaa/1.txt
		      type: FileOrCreate

iscsi

An iscsi volume allows an existing iSCSI (SCSI over IP) volume to be mounted into your Pod. Unlike emptyDir, which is erased when a Pod is removed, the contents of an iscsi volume are preserved and the volume is merely unmounted. This means that an iscsi volume can be pre-populated with data, and that data can be shared between pods.
Note: You must have your own iSCSI server running with the volume created before you can use it.


See the iSCSI example for more details.



local

A local volume represents a mounted local storage device such as a disk, partition or directory.

Local volumes can only be used as a statically created PersistentVolume. Dynamic provisioning is not supported.

Compared to hostPath volumes, local volumes are used in a durable and portable manner without manually scheduling pods to nodes. The system is aware of the volume's node constraints by looking at the node affinity on the 


PersistentVolume.

However, local volumes are subject to the availability of the underlying node and are not suitable for all applications. If a node becomes unhealthy, then the local volume becomes inaccessible by the pod. The pod using this volume is unable to run. Applications using local volumes must be able to tolerate this reduced availability, as well as potential data loss, depending on the durability characteristics of the underlying disk.

The following example shows a PersistentVolume using a local volume and nodeAffinity:

		apiVersion: v1
		kind: PersistentVolume
		metadata:
		  name: example-pv
		spec:
		  capacity:
		    storage: 100Gi
		  volumeMode: Filesystem
		  accessModes:
		  - ReadWriteOnce
		  persistentVolumeReclaimPolicy: Delete
		  storageClassName: local-storage
		  local:
		    path: /mnt/disks/ssd1
		  nodeAffinity:
		    required:
		      nodeSelectorTerms:
		      - matchExpressions:
			- key: kubernetes.io/hostname
			  operator: In
			  values:
			  - example-node

You must set a PersistentVolume nodeAffinity when using local volumes. The Kubernetes scheduler uses the PersistentVolume nodeAffinity to schedule these Pods to the correct node.

PersistentVolume volumeMode can be set to "Block" (instead of the default value "Filesystem") to expose the local volume as a raw block device.



nfs

An nfs volume allows an existing NFS (Network File System) share to be mounted into a Pod. Unlike emptyDir, which is erased when a Pod is removed, the contents of an nfs volume are preserved and the volume is merely unmounted. This means that an NFS volume can be pre-populated with data, and that data can be shared between pods. NFS can be mounted by multiple writers simultaneously.

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-pd
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-container
		    volumeMounts:
		    - mountPath: /my-nfs-data
		      name: test-volume
		  volumes:
		  - name: test-volume
		    nfs:
		      server: my-nfs-server.example.com
		      path: /my-nfs-volume
		      readOnly: true


A portworxVolume can be dynamically created through Kubernetes or it can also be pre-provisioned and referenced inside a Pod. Here is an example Pod referencing a pre-provisioned Portworx volume:

		apiVersion: v1
		kind: Pod
		metadata:
		  name: test-portworx-volume-pod
		spec:
		  containers:
		  - image: registry.k8s.io/test-webserver
		    name: test-container
		    volumeMounts:
		    - mountPath: /mnt
		      name: pxvol
		  volumes:
		  - name: pxvol
		    # This Portworx volume must already exist.
		    portworxVolume:
		      volumeID: "pxvol"
		      fsType: "<fs-type>"

Note: Make sure you have an existing PortworxVolume with name pxvol before using it in the Pod.

For more details, see the Portworx volume examples.
Portworx CSI migration



The PHP application's code and assets map to the volume's html folder and the MySQL database is stored in the volume's mysql folder. For example:

		apiVersion: v1
		kind: Pod
		metadata:
		  name: my-lamp-site
		spec:
		    containers:
		    - name: mysql
		      image: mysql
		      env:
		      - name: MYSQL_ROOT_PASSWORD
			value: "rootpasswd"
		      volumeMounts:
		      - mountPath: /var/lib/mysql
			name: site-data
			subPath: mysql
		    - name: php
		      image: php:7.0-apache
		      volumeMounts:
		      - mountPath: /var/www/html
			name: site-data
			subPath: html
		    volumes:
		    - name: site-data
		      persistentVolumeClaim:
			claimName: my-lamp-site-data


Using subPath with expanded environment variables

Use the subPathExpr field to construct subPath directory names from downward API environment variables. The subPath and subPathExpr properties are mutually exclusive.

In this example, a Pod uses subPathExpr to create a directory pod1 within the hostPath volume /var/log/pods. The hostPath volume takes the Pod name from the downwardAPI. The host directory /var/log/pods/pod1 is mounted at /logs in the container.

		apiVersion: v1
		kind: Pod
		metadata:
		  name: pod1
		spec:
		  containers:
		  - name: container1
		    env:
		    - name: POD_NAME
		      valueFrom:
			fieldRef:
			  apiVersion: v1
			  fieldPath: metadata.name
		    image: busybox:1.28
		    command: [ "sh", "-c", "while [ true ]; do echo 'Hello'; sleep 10; done | tee -a /logs/hello.txt" ]
		    volumeMounts:
		    - name: workdir1
		      mountPath: /logs
		      # The variable expansion uses round brackets (not curly brackets).
		      subPathExpr: $(POD_NAME)
		  restartPolicy: Never
		  volumes:
		  - name: workdir1
		    hostPath:
		      path: /var/log/pods

Resources

The storage media (such as Disk or SSD) of an emptyDir volume is determined by the medium of the filesystem holding the kubelet root dir (typically /var/lib/kubelet). There is no limit on how much space an emptyDir or hostPath volume can consume, and no isolation between containers or between pods.







[Got To Top](#top)
<a name="configmap"></a>
# ConfigMap

     ***Tested Example By Ajay Sisaudiya***
	
	
1. 	
	
    CMDS:
	
	Creating CinfigMap: 
	
	microk8s kubectl create configmap envcm01 --from-literal="astechutube" --from-literal="abc123" 
 	 or  
	microk8s kubectl create cm envcm01 --from-literal="astechutube" --from-literal="abc123"
	microk8s kubectl get cm
	microk8s kubectl describe cm envcm01

	microk8s kubectl explain --recursive pod
	microk8s kubectl explain --recursive pod | less

  
	
 cm01-pod.yml  (Only One Value)

	
	apiVersion: v1 
	kind: Pod
	metadata: 
	   name: cm01-pod
	spec: 
	  containers: 
	  - name: cm01-pod
	    image: nginx
	    imagePullPolicy: Never
	    env: 
	     - name: varsfromcm
	       valueFrom:
		 configMapKeyRef:
		    key: name
		    name: envcm01 

            
   OR         
	
 #           
	
2. ***cm01-pod.yml (Only Two Values)***

	
	
		apiVersion: v1 
		kind: Pod
		metadata: 
		   name: cm01-pod
		spec: 
		  containers: 
		  - name: cm01-pod
		    image: nginx
		    imagePullPolicy: Never
		    env: 
		     - name: varsfromcm1
		       valueFrom:
			 configMapKeyRef:
			    key: name
			    name: envcm01 
		     - name: varsfromcm2
		       valueFrom:
			 configMapKeyRef:
			    key: password
			    name: envcm01 


            
  CMDS: 
	microk8s kubectl apply -f cm01-pod.yml      
	microk8s kubectl exec -it cm01-pod bash  
	root@cm01-pod:/# env
	
	
#	
	
3. ***Using Yaml File***	

   fromfilemc01.yml
	
	
		apiVersion: v1
		kind: ConfigMap
		metadata:
		  name: fromfilecm01
		data:
		  #property-like keys; each key maps to a simple value
		  #player_initial_lives: "3"
		  #ui_properties_file_name: "user-interface.properties"

		  #file-like keys
		  env.sh: |
		    name=ajay
		    age=88
		    city=meerut
		    country=india

	
	
     CMDS:
	
	microk8s kubectl apply -f fromfilecm01.yml
	
	
	
cm01-pod.yml
	
	
		apiVersion: v1
		kind: Pod
		metadata:
		   name: cm01-pod
		spec:
		  containers:
		  - name: cm01-pod
		    image: nginx
		    imagePullPolicy: Never
		    env:
		     - name: varsfromcm1
		       valueFrom:
			 configMapKeyRef:
			    key: name
			    name: envcm01
		     - name: varsfromcm2
		       valueFrom:
			 configMapKeyRef:
			    key: password
			    name: envcm01
		     - name: varsfromfile3
		       valueFrom:
			 configMapKeyRef:
			    key: env.sh
			    name: fromfilecm01


	
	
  CMDS: 
	microk8s kubectl apply -f cm01-pod.yml      
	microk8s kubectl exec -it cm01-pod bash  
	root@cm01-pod:/# env
	
	
	
	
4. ***Using envFrom & configMapRef (Including configMap File***	

	

    fromfilemc01.yml
	
	
	
		apiVersion: v1
		kind: ConfigMap
		metadata:
		  name: fromfilecm01
		data:
		  #property-like keys; each key maps to a simple value
		  #player_initial_lives: "3"
		  #ui_properties_file_name: "user-interface.properties"

		  #file-like keys
		  env.sh: |
		    name=ajay
		    age=88
		    city=meerut
		    country=india

	
	
     CMDS:
	
	microk8s kubectl apply -f fromfilecm01.yml
	
	
	
	
cm01-pod.yml
	

		apiVersion: v1 
		kind: Pod
		metadata: 
		   name: cm01-pod
		spec: 
		  containers: 
		  - name: cm01-pod
		    image: nginx
		    imagePullPolicy: Never         
		    envFrom:
		      - configMapRef:           
			  name: fromfilecm 


	

	microk8s kubectl apply -f cm01-pod.yml      
	microk8s kubectl exec -it cm01-pod bash  
	root@cm01-pod:/# env	


	
	
:end:	
	
	
#	
	
	How to Create a ConfigMap?
	
	kubectl create configmap [configmap_name] [attribute] [source]	
	
	  --from file (if the source is a file/directory)
	  --from-literal (if the source is a key-value pair)	

	
	apiVersion: v1
	data:
	  key1: value1
	  key2: value2
	  ...
	kind: ConfigMap
	metadata:
	  creationTimeStamp: ...
	  name: example-configmap
	  namespace: default
	  resourceVersion: ...
	  selfLink: /api/v1/namespace/default/configmaps/example-configmap
	  uid: ...
	
	
	
Mounting ConfigMap as a Volume:	

	
	Add a volume section to the to the yaml file of your pod:

	volumes:
	  - name: config
	  configMap
	    name: [configmap_name]
	    items:
	    - key: [key/file_name]
	    path: [inside_the_pod]

	
Use ConfigMap with EnvFrom
	
	
	env:
		- name: SPECIAL_LEVEL_KEY
		  valueFrom:
		    configMapKeyRef:
		      name: [configmap_name]
		      key: [key/file_name]	

	
	
To pull all environment variables from a ConfigMap, add the envFrom section to the yaml file:

	envFrom:
	  - configMapKeyRef
	      name: env-config	


	
	
	apiVersion: v1
	kind: ConfigMap	
	metadata:
	  name: mysql-config
	data:
	  confluence.cnf: |-
	    [mysqld]
	    bind-address     = 0.0.0.0
	    character-set-server=utf8
	    collation-server=utf8_bin
	    default-storage-engine=INNODB
	    max_allowed_packet=256M
	    innodb_log_file_size=2GB
	    transaction-isolation=READ-COMMITTED
	
	
ConfigMaps

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.


ConfigMaps and Pods:

Here's an example ConfigMap that has some keys with single values, and other keys where the value looks like a fragment of a configuration format.


		apiVersion: v1
		kind: ConfigMap
		metadata:
		  name: game-demo
		data:
		  #property-like keys; each key maps to a simple value
		  player_initial_lives: "3"
		  ui_properties_file_name: "user-interface.properties"

		  #file-like keys
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
<a name="secrets"></a>
# Secrets

	
CMDS:
	

		microk8s kubectl explain secret      
		microk8s kubectl api-resources | grep -i sec
		microk8s kubectl create secret --help
		microk8s kubectl create secret generic --help | less

		microk8s kubectl create secret generic first --from-literal=name=ajay
		or 
		microk8s kubectl create secret generic myfilesec --from-file

		microk8s kubectl get secrets
		microk8s kubectl describe secret first
		microk8s kubectl get secrets first
		microk8s kubectl get secrets first -o yaml
		echo -n "ajay" | base64




#
A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.


This is an example of a Pod that mounts a Secret named mysecret in a volume:

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
		    secret:
		      secretName: mysecret
		      optional: false # default setting; "mysecret" must exist




Projection of Secret keys to specific paths:


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
		    secret:
		      secretName: mysecret
		      items:
		      - key: username
			path: my-group/my-username		
			
  
  
  
      
      
Secret files permissions:
 
		 
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
		  volumes:
		  - name: foo
		    secret:
		      secretName: mysecret
		      defaultMode: 0400
     
      
      
      
     Consuming Secret values from volumes
     ls /etc/foo/
     cat /etc/foo/username
     cat /etc/foo/password  
          
    

Using Secrets as environment variables:


		apiVersion: v1
		kind: Pod
		metadata:
		  name: secret-env-pod
		spec:
		  containers:
		  - name: mycontainer
		    image: redis
		    env:
		      - name: SECRET_USERNAME
			valueFrom:
			  secretKeyRef:
			    name: mysecret
			    key: username
			    optional: false # same as default; "mysecret" must exist
				            # and include a key named "username"
		      - name: SECRET_PASSWORD
			valueFrom:
			  secretKeyRef:
			    name: mysecret
			    key: password
			    optional: false # same as default; "mysecret" must exist
				            # and include a key named "password"
		  restartPolicy: Never






kubectl get events



Use cases
Use case: As container environment variables

Create a secret

		apiVersion: v1
		kind: Secret
		metadata:
		  name: mysecret
		type: Opaque
		data:
		  USER_NAME: YWRtaW4=
		  PASSWORD: MWYyZDFlMmU2N2Rm




    	kubectl apply -f mysecret.yaml      
          
          
		apiVersion: v1
		kind: Pod
		metadata:
		  name: secret-test-pod
		spec:
		  containers:
		    - name: test-container
		      image: registry.k8s.io/busybox
		      command: [ "/bin/sh", "-c", "env" ]
		      envFrom:
		      - secretRef:
			  name: mysecret
		  restartPolicy: Never
			  
          
          
Use case: Pod with SSH keys

Create a Secret containing some SSH keys:

		kubectl create secret generic ssh-key-secret --from-file=ssh-privatekey=/path/to/.ssh/id_rsa --from-file=ssh-publickey=/path/to/.ssh/id_rsa.pub



Now you can create a Pod which references the secret with the SSH key and consumes it in a volume:

		apiVersion: v1
		kind: Pod
		metadata:
		  name: secret-test-pod
		  labels:
		    name: secret-test
		spec:
		  volumes:
		  - name: secret-volume
		    secret:
		      secretName: ssh-key-secret
		  containers:
		  - name: ssh-test-container
		    image: mySshImage
		    volumeMounts:
		    - name: secret-volume
		      readOnly: true
		      mountPath: "/etc/secret-volume"


          


When the container's command runs, the pieces of the key will be available in:

		/etc/secret-volume/ssh-publickey
		/etc/secret-volume/ssh-privatekey




Use case: Pods with prod / test credentials



		kubectl create secret generic prod-db-secret --from-literal=username=produser --from-literal=password=Y4nys7f11



You can also create a secret for test environment credentials.

		kubectl create secret generic test-db-secret --from-literal=username=testuser --from-literal=password=iluvtests



		kubectl create secret generic dev-db-secret --from-literal=username=devuser --from-literal=password='S!B\*d$zDsb='




Now make the Pods:

		cat <<EOF > pod.yaml
		apiVersion: v1
		kind: List
		items:
		- kind: Pod
		  apiVersion: v1
		  metadata:
		    name: prod-db-client-pod
		    labels:
		      name: prod-db-client
		  spec:
		    volumes:
		    - name: secret-volume
		      secret:
			secretName: prod-db-secret
		    containers:
		    - name: db-client-container
		      image: myClientImage
		      volumeMounts:
		      - name: secret-volume
			readOnly: true
			mountPath: "/etc/secret-volume"
		- kind: Pod
		  apiVersion: v1
		  metadata:
		    name: test-db-client-pod
		    labels:
		      name: test-db-client
		  spec:
		    volumes:
		    - name: secret-volume
		      secret:
			secretName: test-db-secret
		    containers:
		    - name: db-client-container
		      image: myClientImage
		      volumeMounts:
		      - name: secret-volume
			readOnly: true
			mountPath: "/etc/secret-volume"
		EOF

		Add the pods to the same kustomization.yaml:

		cat <<EOF >> kustomization.yaml
		resources:
		- pod.yaml
		EOF





Apply all those objects on the API server by running:

kubectl apply -k .




Both containers will have the following files present on their filesystems with the values for each container's environment:

	/etc/secret-volume/username
	/etc/secret-volume/password




    prod-user with the prod-db-secret
    test-user with the test-db-secret

The Pod specification is shortened to:

		apiVersion: v1
		kind: Pod
		metadata:
		  name: prod-db-client-pod
		  labels:
		    name: prod-db-client
		spec:
		  serviceAccount: prod-db-client
		  containers:
		  - name: db-client-container
		    image: myClientImage






Use case: dotfiles in a secret volume:



		apiVersion: v1
		kind: Secret
		metadata:
		  name: dotfile-secret
		data:
		  .secret-file: dmFsdWUtMg0KDQo=
		---
		apiVersion: v1
		kind: Pod
		metadata:
		  name: secret-dotfiles-pod
		spec:
		  volumes:
		  - name: secret-volume
		    secret:
		      secretName: dotfile-secret
		  containers:
		  - name: dotfile-test-container
		    image: registry.k8s.io/busybox
		    command:
		    - ls
		    - "-l"
		    - "/etc/secret-volume"
		    volumeMounts:
		    - name: secret-volume
		      readOnly: true
		      mountPath: "/etc/secret-volume"
		      
		      
		      



Types of Secret:



	Built-in Type	Usage
	Opaque	arbitrary user-defined data
	kubernetes.io/service-account-token	ServiceAccount token
	kubernetes.io/dockercfg	serialized ~/.dockercfg file
	kubernetes.io/dockerconfigjson	serialized ~/.docker/config.json file
	kubernetes.io/basic-auth	credentials for basic authentication
	kubernetes.io/ssh-auth	credentials for SSH authentication
	kubernetes.io/tls	data for a TLS client or server
	bootstrap.kubernetes.io/token	bootstrap token data




Opaque secrets



		kubectl create secret generic empty-secret
		kubectl get secret empty-secret




		Service account token Secrets


The following example configuration declares a service account token Secret:

		apiVersion: v1
		kind: Secret
		metadata:
		  name: secret-sa-sample
		  annotations:
		    kubernetes.io/service-account.name: "sa-name"
		type: kubernetes.io/service-account-token
		data:
		  # You can include additional key value pairs as you do with Opaque Secrets
		  extra: YmFyCg==






Docker config Secrets:


    	    kubernetes.io/dockercfg
	    kubernetes.io/dockerconfigjson



Below is an example for a kubernetes.io/dockercfg type of Secret:

		apiVersion: v1
		kind: Secret
		metadata:
		  name: secret-dockercfg
		type: kubernetes.io/dockercfg
		data:
		  .dockercfg: |
			"<base64 encoded ~/.dockercfg file>"



kubectl create secret docker-registry secret-tiger-docker \
  --docker-email=tiger@acme.example \
  --docker-username=tiger \
  --docker-password=pass1234 \
  --docker-server=my-registry.example:5000


kubectl get secret secret-tiger-docker -o jsonpath='{.data.*}' | base64 -d


then the output is equivalent to this JSON document (which is also a valid Docker configuration file):

		{
		  "auths": {
		    "my-registry.example:5000": {
		      "username": "tiger",
		      "password": "pass1234",
		      "email": "tiger@acme.example",
		      "auth": "dGlnZXI6cGFzczEyMzQ="
		    }
		  }
		}







The following manifest is an example of a basic authentication Secret:

		apiVersion: v1
		kind: Secret
		metadata:
		  name: secret-basic-auth
		type: kubernetes.io/basic-auth
		stringData:
		  username: admin      # required field for kubernetes.io/basic-auth
		  password: t0p-Secret # required field for kubernetes.io/basic-auth





The following manifest is an example of a Secret used for SSH public/private key authentication:

		apiVersion: v1
		kind: Secret
		metadata:
		  name: secret-ssh-auth
		type: kubernetes.io/ssh-auth
		data:
		  # the data is abbreviated in this example
		  ssh-privatekey: |
			  MIIEpQIBAAKCAQEAulqb/Y ...



The following YAML contains an example config for a TLS Secret:

		apiVersion: v1
		kind: Secret
		metadata:
		  name: secret-tls
		type: kubernetes.io/tls
		data:
		  # the data is abbreviated in this example
		  tls.crt: |
			MIIC2DCCAcCgAwIBAgIBATANBgkqh ...
		  tls.key: |
			MIIEpgIBAAKCAQEA7yn3bRHQ5FHMQ ...




		kubectl create secret tls my-tls-secret \
		  --cert=path/to/cert/file \
		  --key=path/to/key/file
		  
  
  



As a Kubernetes manifest, a bootstrap token Secret might look like the following:

		apiVersion: v1
		kind: Secret
		metadata:
		  name: bootstrap-token-5emitj
		  namespace: kube-system
		type: bootstrap.kubernetes.io/token
		data:
		  auth-extra-groups: c3lzdGVtOmJvb3RzdHJhcHBlcnM6a3ViZWFkbTpkZWZhdWx0LW5vZGUtdG9rZW4=
		  expiration: MjAyMC0wOS0xM1QwNDozOToxMFo=
		  token-id: NWVtaXRq
		  token-secret: a3E0Z2lodnN6emduMXAwcg==
		  usage-bootstrap-authentication: dHJ1ZQ==
		  usage-bootstrap-signing: dHJ1ZQ==


In fact, you can create an identical Secret using the following YAML:

		apiVersion: v1
		kind: Secret
		metadata:
		  # Note how the Secret is named
		  name: bootstrap-token-5emitj
		  # A bootstrap token Secret usually resides in the kube-system namespace
		  namespace: kube-system
		type: bootstrap.kubernetes.io/token
		stringData:
		  auth-extra-groups: "system:bootstrappers:kubeadm:default-node-token"
		  expiration: "2020-09-13T04:39:10Z"
		  # This token ID is used in the name
		  token-id: "5emitj"
		  token-secret: "kq4gihvszzgn1p0r"
		  # This token can be used for authentication
		  usage-bootstrap-authentication: "true"
		  # and it can be used for signing
		  usage-bootstrap-signing: "true"





Marking a Secret as immutable

You can create an immutable Secret by setting the immutable field to true. For example,


		apiVersion: v1
		kind: Secret
		metadata:
		  ...
		data:
		  ...
		immutable: true






[Got To Top](#top)
<a name="clusterip"></a>
# ClusterIP


Service ClusterIP allocation:



How Service ClusterIPs are allocated?

	dynamically
	statically



Why do you need to reserve Service Cluster IPs?

Sometimes you may want to have Services running in well-known IP addresses, so other components and users in the cluster can use them.

The best example is the DNS Service for the cluster. As a soft convention, some Kubernetes installers assign the 10th IP address from the Service IP range to the DNS service. Assuming you configured your cluster with Service IP range 10.96.0.0/16 and you want your DNS Service IP to be 10.96.0.10, you'd have to create a Service like this:



		apiVersion: v1
		kind: Service
		metadata:
		  labels:
		    k8s-app: kube-dns
		    kubernetes.io/cluster-service: "true"
		    kubernetes.io/name: CoreDNS
		  name: kube-dns
		  namespace: kube-system
		spec:
		  clusterIP: 10.96.0.10
		  ports:
		  - name: dns
		    port: 53
		    protocol: UDP
		    targetPort: 53
		  - name: dns-tcp
		    port: 53
		    protocol: TCP
		    targetPort: 53
		  selector:
		    k8s-app: kube-dns
		  type: ClusterIP



How can you avoid Service ClusterIP conflicts?

The allocation strategy implemented in Kubernetes to allocate ClusterIPs to Services reduces the risk of collision.

The ClusterIP range is divided, based on the formula min(max(16, cidrSize / 16), 256), described as never less than 16 or more than 256 with a graduated step between them.

Dynamic IP assignment uses the upper band by default, once this has been exhausted it will use the lower range. This will allow users to use static allocations on the lower band with a low risk of collision.
 















[Got To Top](#top)
<a name="headless"></a>
# Headless 

Headless Services

Sometimes you don't need load-balancing and a single Service IP. In this case, you can create what are termed "headless" Services, by explicitly specifying "None" for the cluster IP (.spec.clusterIP).

You can use a headless Service to interface with other service discovery mechanisms, without being tied to Kubernetes' implementation.

For headless Services, a cluster IP is not allocated, kube-proxy does not handle these Services, and there is no load balancing or proxying done by the platform for them. How DNS is automatically configured depends on whether the Service has selectors defined:
With selectors

For headless Services that define selectors, the Kubernetes control plane creates EndpointSlice objects in the Kubernetes API, and modifies the DNS configuration to return A or AAAA records (IPv4 or IPv6 addresses) that point directly to the Pods backing the Service.
Without selectors

For headless Services that do not define selectors, the control plane does not create EndpointSlice objects. However, the DNS system looks for and configures either:

    DNS CNAME records for type: ExternalName Services.
    DNS A / AAAA records for all IP addresses of the Service's ready endpoints, for all Service types other than ExternalName.
        For IPv4 endpoints, the DNS system creates A records.
        For IPv6 endpoints, the DNS system creates AAAA records.
        
        

What is a Headless Service?

When there is no need of load balancing or single-service IP addresses.We create a headless service which is used for creating a service grouping. That does not allocate an IP address or forward traffic.So you can do this by explicitly setting ClusterIP to “None” in the mainfest file, which means no cluster IP is allocated.


        
 Use Cases of Headless Service-

    Create Stateful service
    Deploying RabbitMQ to Kubernetes requires a stateful set for RabbitMQ cluster nodes.
    Deployment of Relational databases

Deployment manifest file:-

		apiVersion: apps/v1
		kind: Deployment
		metadata:
		  name: app
		  labels:
		    app: server
		spec:
		  replicas: 3
		  selector:
		    matchLabels:
		      app: web
		  template:
		    metadata:
		      labels:
			app: web
		    spec:
		      containers:
		      - name: nginx
			image: nginx
			ports:
			- containerPort: 80

		Regular Service:-

		apiVersion: v1
		kind: Service
		metadata:
		  name: regular-service
		spec:
		  selector:
		    app: web
		  ports:
		    - protocol: TCP
		      port: 80
		      targetPort: 8080

		Headless Service:-

		apiVersion: v1
		kind: Service
		metadata:
		  name: headless-svc
		spec:
		  clusterIP: None 
		  selector:
		    app: web
		  ports:
		    - protocol: TCP
		      port: 80
		      targetPort: 8080



	Create all resources and run the pod

	kubectl create -f deployment.yaml

	kubectl create -f regular-service.yaml

	kubectl create -f headless-service.yaml

	kubectl run temporary --image=radial/busyboxplus:curl -i --tty

	Cleanup the used resources

	kubectl delete svc regular-service

	kubectl delete svc headless-svc

	kubectl delete deployment app

	kubectl delete po temporary

	
The DNS server returns three different IPs for the pods

   
        
        
        



	
	
	

[Got To Top](#top)
<a name="multi-port"></a>
# Multi-Port 



Multi-Port Services

For some Services, you need to expose more than one port. Kubernetes lets you configure multiple port definitions on a Service object. When using multiple ports for a Service, you must give all of your ports names so that these are unambiguous. For example:

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

Note:

As with Kubernetes names in general, names for ports must only contain lowercase alphanumeric characters and -. Port names must also start and end with an alphanumeric character.






How to expose multiple port in services in kubernetes or Multi-Port Services

names so that these are unambiguous. For example:

		apiVersion: v1
		kind: Service
		metadata:
		  name: my-service
		spec:
		  selector:
		    app: MyApp
		  ports:
		    - name: http
		      protocol: TCP
		      port: 80
		      targetPort: 9376
		    - name: https
		      protocol: TCP
		      port: 443
		      targetPort: 9377



How to work with command line?

	kubectl create service  clusterip svc3 --tcp=8080:80 --tcp=8090:80

service/svc3 created

	kubectl describe svc svc3
	
	
	


[Got To Top](#top)
<a name="nodeport"></a>
# NodePort 


Type NodePort

If you set the type field to NodePort, the Kubernetes control plane allocates a port from a range specified by --service-node-port-range flag (default: 30000-32767). Each node proxies that port (the same port number on every Node) into your Service. Your Service reports the allocated port in its .spec.ports[*].nodePort field.

Using a NodePort gives you the freedom to set up your own load balancing solution, to configure environments that are not fully supported by Kubernetes, or even to expose one or more nodes' IP addresses directly.

For a node port Service, Kubernetes additionally allocates a port (TCP, UDP or SCTP to match the protocol of the Service). Every node in the cluster configures itself to listen on that assigned port and to forward traffic to one of the ready endpoints associated with that Service. You'll be able to contact the type: NodePort Service, from outside the cluster, by connecting to any node using the appropriate protocol (for example: TCP), and the appropriate port (as assigned to that Service).
Choosing your own port

If you want a specific port number, you can specify a value in the nodePort field. The control plane will either allocate you that port or report that the API transaction failed. This means that you need to take care of possible port collisions yourself. You also have to use a valid port number, one that's inside the range configured for NodePort use.

Here is an example manifest for a Service of type: NodePort that specifies a NodePort value (30007, in this example).

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



Custom IP address configuration for type: NodePort Services

You can set up nodes in your cluster to use a particular IP address for serving node port services. You might want to do this if each node is connected to multiple networks (for example: one network for application traffic, and another network for traffic between nodes and the control plane).

If you want to specify particular IP address(es) to proxy the port, you can set the --nodeport-addresses flag for kube-proxy or the equivalent nodePortAddresses field of the kube-proxy configuration file to particular IP block(s).

This flag takes a comma-delimited list of IP blocks (e.g. 10.0.0.0/8, 192.0.2.0/25) to specify IP address ranges that kube-proxy should consider as local to this node.

For example, if you start kube-proxy with the --nodeport-addresses=127.0.0.0/8 flag, kube-proxy only selects the loopback interface for NodePort Services. The default for --nodeport-addresses is an empty list. This means that kube-proxy should consider all available network interfaces for NodePort. (That's also compatible with earlier Kubernetes releases.)
Note: This Service is visible as <NodeIP>:spec.ports[*].nodePort and .spec.clusterIP:spec.ports[*].port. If the --nodeport-addresses flag for kube-proxy or the equivalent field in the kube-proxy configuration file is set, <NodeIP> would be a filtered node IP address (or possibly IP addresses).


[Got To Top](#top)
<a name="statefullset"></a>
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
<a name="loadbalancer"></a>
# LoadBalancer

Type LoadBalancer

On cloud providers which support external load balancers, setting the type field to LoadBalancer provisions a load balancer for your Service. The actual creation of the load balancer happens asynchronously, and information about the provisioned balancer is published in the Service's .status.loadBalancer field. For example:

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





#
[Got To Top](#top)
<a name="jobs"></a>
# Jobs

	
	
	
	
