<!-- # Kubernetes Commands & Examples For Beginners -->
$$\large{\colorbox{black}{\color{red}Kubernetes \ Commands \ and \ Examples \ For \ Beginners}}$$

:link:[Home](all-file-links.md)     




<a name="top"></a>
## Topics 


###### 1. Basic Commands [Go to Basic Commands click here](#basic_commands) 
###### 2. Minikube [Go to Minikube click here](#minikube)
###### 3. KubeCTL [Go to Kubectl click here](#kubectl)
###### 4. Create YML File [Go to Create YML File click here](#create_yml_file)
###### 5. Microk8s CMDS [Go to Microk8s click here](#micro8ks_cmds)
###### 5. Microk8s CMDS [Go to Installation Minikube on Ubuntu click here](#install_minikube)
  
###### 6. Microk8s CMDS [Go To Nodes on Ubuntu click here](#nodes)
###### 7. Microk8s CMDS [Go To Namespaces(nc) on Ubuntu click here](#namespaces)
###### 8. Microk8s CMDS [Go To Pods(po) on Ubuntu click here](#pods)
###### 9. Microk8s CMDS [Go To Deployment(deploy) on Ubuntu click here](#deployment)
###### 10. Microk8s CMDS [Go To Services(svc) on Ubuntu click here](#services)
###### 11. Microk8s CMDS [Go To Replicas(rc) on Ubuntu click here](#replicas)
###### 12. Microk8s CMDS [Pod yml,deployment yml,service yml file click here](#yml_files)

###### 12. Microk8s CMDS [Node yml file click here](#yml_nodes)
###### 12. Microk8s CMDS [Pod yml file click here](#yml_pods)
###### 12. Microk8s CMDS [Deployment yml click here](#yml_deployment)
###### 12. Microk8s CMDS [Service yml file click here](#yml_service)
###### 12. Microk8s CMDS [Replicaset yml file click here](#yml_replicaset)

###### 13. Microk8s CMDS [The connection to the server 127.0.0.1:16443 was refused - did you specify the right host or port? on Ubuntu click here](#replicas)

	


[Go To Top](#top)
<!----><a name="basic_commands"></a>
### Basic Commands 

	0. Display all list (pods,services,deployments & riplicaSets)
	   kubectl get all --all-namespaces  
	   microk8s enable dns storage           //Use add-ons


	1. Run a yamal file

	   //Output redirect to new yaml file
	   kubectl run secondpod --dry-run --generator=run-pod/v1 --image=coolgaurab147/nginx-custom -o yaml > mysecondpd.yml

	   kubectl create -f firstpod.yml --dry-run
	   kubectl apply -f firstpod.yml
	   cat myfirstpod.yml
	   kubectl create -f firstpod.yml

	2. Pods
	   kubectl get pods
	   kubectl delete pod myfirstpod
	   kubectl explain pod --recursive !less

	   kubectl run secondpod --generator=run-pod/v1 --image=coolgaurab147/nginx-custom
	   //Client side run 
	   kubectl run secondpod --dry-run --generator=run-pod/v1 --image=coolgaurab147/nginx-custom
	   kubectl run secondpod --dry-run --generator=run-pod/v1 --image=coolgaurab147/nginx-custom -o yaml


	3. Services
	   kubectl get services

	4. Deployment

	   kubectl get pods
	   kubectl create deployment <deploymentName> --image=nginx
	   kubectl create deployment <deploymentName> --image=mysql --replicas=2
	   kubectl scale deployment <deploymentName> --replicas=1
	   kubectl get deployments
	   kubectl get deployments -o wide
	   kubectl get deployments -o yaml 
	   kubectl get deployments -o json
	   kubectl describe deployment
	   kubectl describe deployment <deploymentName>
	   kubectl rollout undo deployment <deploymentName> --to-revision=1
	   
     	   
	   
	   
[Go To Top](#top)	   
## Minikube & KubeCTL

	What is Minikube
	Minikube installation steps in windows
	How to deploy first spring boot application to Kubernetes


Installatioin: 

	1. Minikube     (  )
	2. KubeCTL      (  )

Requirements:

	  1. Virtual Box Or Hiper-V or docker ( as a driver )





[Go To Top](#top)
<!----><a name="minikube"></a>
### 1. Minikube Installation ( minikube.exe )

	   Usually used to run k8s cluster in your local machine/computer.
	   Minikube runs a single-node Kubernetes cluster on your machine so that you can try out Kubernetes for your daily development work.
	   Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one  node.
	
	
	
	
	
[Go To Top](#top)	
<!----><a name="kubectl"></a>
### 2. KubeCtl Installation ( Kubectl.exe )

	kubectl. The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs. For more information including a complete list of kubectl operations, see the kubectl reference documentation.

  Download minikube & kubectl
  
  Install first minikube second kubectl
  
  Path to environment variable  ( kubectl & minikube )

	  Open cmd write command 
		    > minikube start --driver=docker
		    > minikube status
		    > kubectl cluster-info
		    > kubectl get node

	    Now install spring boot project

		    > minikube docker-env
		    > copy the above command showing @FOR /F %1 ('minikube -p minikube docker-env') Do @i
		    > docker images
		    > ........... more
		    
		
		
 
 
 [Go To Top](#top)
 <!----><a name="create_yml_file"></a>
 ### Create Yaml File

   MyFirst Yaml File:

	apiVersion: 
	kind: 
	metadata:
	spec:


	apiVersion: v1
	kind: Pod

	metadata:
	 name: myfirstpod
	 labels: 
	  env:prod

	spec:
	 containers:
	  - name: containername
	    image: coolgaurab147/nginx-custom


	 Run Yamal File: 
	 kubectl create -f firstpod.yml --dry-run
	 cat myfirstpod.yml
	 kubectl create -f firstpod.yml
	 kubectl get pods
	 kubectl explain pod --recursive !less


#basic-commands
This is heading 


 //Create k8s pod
 
	 kubectl run secondpod --generator=run-pod/v1 --image=coolgaurab147/nginx-custom
	 //Client side run 
	 kubectl run secondpod --dry-run --generator=run-pod/v1 --image=coolgaurab147/nginx-custom
	 kubectl run secondpod --dry-run --generator=run-pod/v1 --image=coolgaurab147/nginx-custom -o yaml

 //Output redirect to new yaml file
 
  	kubectl run secondpod --dry-run --generator=run-pod/v1 --image=coolgaurab147/nginx-custom -o yaml > mysecondpd.yml
    
  Commands: 
	  kubectl get pods
	  kubectl delete pods myfirstpod
	  ls
	  kubectl apply -f mysecond.yml    //Create pod   

 Example YML File: 
	
	 apiVersion: apps/v1
	kind: Deployment
	metadata:
	  name: nginx
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
		image: nginx:1.7.9
		ports:
		- containerPort: 80 
 
 
 
 
 
 [Go To Top](#top)
<!----><a name="micro8ks_cmds"></a>
 ### Microk8s CMDS
 
	 sudo snap install microk8s --classic --channel=1.25   //Install MicroK8s
	 sudo usermod -a -G microk8s $USER                    //Join the group
	 sudo chown -f -R $USER ~/.kube
	 su - $USER                                           // Password
	 microk8s status --wait-ready                         //Check the status
	 microk8s kubectl get nodes                          //Access Kubernetes
	 microk8s kubectl get services
	 alias kubectl='microk8s kubectl'

	 microk8s kubectl create deployment nginx --image=nginx //Deploy an app
	 microk8s kubectl get pods

	 microk8s enable dns storage           //Use add-ons



[Go To Top](#top)
  //microk8s
	
	  microk8s stop
	  microk8s start
	  microk8s status
	  microk8s kubectl get all --all-namespaces
	  microk8s kubectl get pods
	  microk8s kubectl create deployment <deploymentName> --image=nginx
	  microk8s kubectl create deployment <deploymentName> --image=mysql --replicas=2
	  microk8s kubectl scale deployment <deploymentName> --replicas=1
	  microk8s kubectl get deployments
	  microk8s kubectl get deployments -o wide
	  microk8s kubectl get deployments -o yaml 
	  microk8s kubectl get deployments -o json
	  microk8s kubectl describe deployment
	  microk8s kubectl describe deployment <deploymentName>
	  microk8s kubectl rollout undo deployment <deploymentName> --to-revision=1




[Go To Top](#top)
//In Pod's container
	
	kubectl get pods
	kubectl exec <podName> env
	kubectl exec <podName> -c <containerName> env
	kubectl exec <podName> 
	kucbctl get pods
	kubectl exec <podName> <containerName> -it bash
	kubectl exec <podName> -c <containerName> -it bash
	kubectl exec <podName> -c <containerName> -it ls /   

Some CMDS: 
	
	kubectl expose pod <podName>
	kubectl get pod
	kubectl expose pod <podname> --port=8000 --target=80 --name <serviceName>
	kubectl get services
	kubectl get svc
	curl 10.88.20e.56:8000

//Mulit containers in a pod (shared network)
	
	kubectl get pods
	kubectl apply -f firstpod.yml
	kubectl get pods

	kubectl grep name firstpod.yml
	kubectl exec myfirstpod -c firstcontainer -it bash
	netstat -nltp
	netcat -l -p 8000  //Port listen
	telnet localhost 8000
	ifconfig

//initContainer (Add initContainer in above yml file)
	
	 initContainers:
	  - name: initcontainer
	    image: coolgourav147/nginx-custom
	    env:
	     - name: myname
	       value: Gaurav
	     - name: City
	       value: Jaipur
	    args: ["sleep","3600"]
	  - name: secondcontainer
	    image: coolgourav147/nginx-custom  

	kubectl apply -f firtpod.yml
	kubectl get pods -w






[Go To Top](#top)
  ###### Kubernetes Short Commands:
  
  Minikube vs Kind vs K3s 
   
	  kubectl get all
	  kubectl get rs
	  kubectl get ns
	  kubectl get pods -n kube-system    

	  Minikube: 
	  minikube kubectl get all
	  minikube kubectl get rs
	  minikube kubectl get ns
	  minikube kubectl get pods -n kube-system

	  kind kubectl get all
	  kind kubectl get rs
	  kind kubectl get ns
	  kind kubectl get pods -n kube-system

	  microk8s kubectl get all
	  microk8s kind kubectl get rs
	  microk8s kind kubectl get ns
	  microk8s kind kubectl get pods -n kube-system
 
   



[Go To Top](#top)
<!----><a name="install_minikube"></a>
 Installation Minikube on ubuntu
 
 Minikube System Requirements

    2 GB RAM or more
    2 CPU / vCPU or more
    20 GB free hard disk space or more
    Docker / Virtual Machine Manager – KVM & VirtualBox

 Prerequisites for minikube

    Minimal Ubuntu 20.04 LTS / 21.04
    Sudo User with root privileges
    Stable Internet Connection

Step 1) Apply updates: 
        Apply all updates of existing packages of your system by executing the following apt commands,
 
   sudo apt update -y 
   sudo apt upgrade -y
  
 Once all the updates are installed then reboot your system once.
  sudo reboot
 
Step 2) Install Minikube dependencies
         Install the following minikube dependencies by running beneath command,
	 
   sudo apt install -y curl wget apt-transport-https
 
Step 3) Download Minikube Binary
        Download Minikube latest minikube binary       

 	 wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

       Once the binary is downloaded, copy it to the path /usr/local/bin and set the executable permissions on it

		 sudo cp minikube-linux-amd64 /usr/local/bin/minikube
		 sudo chmod +x /usr/local/bin/minikube 

       Verify the minikube version
       
	  minikube version
	  minikube version: v1.27.0                          
	  commit: 4243041b7a72319b9be7842a7d34b6767bbdac2b  

       
Step 4) Install Kubectl utility
 	Kubectl is a command line utility which is used to interact with Kubernetes cluster. It is used for managing deployments, service and pods etc. Use below curl command to download latest version of kubectl.
 
 
    	curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl     
    
    
       Once kubectl is downloaded then set the executable permissions on kubectl binary and move it to the path /usr/local/bin.    
    
    
	  chmod +x kubectl                      
	  sudo mv kubectl /usr/local/bin/       
    
       Now verify the kubectl version    
    
	  kubectl version -o yaml              
  
 Step 5) Start minikube
         As we are already stated in the beginning that we would be using docker as base for minikue, so start the minikube with the docker driver, run 
  
  minikube start --driver=docker      
  
  
 In case you want to start minikube with customize resources and want installer to automatically select the driver then you can run following command,
 
  	minikube start --addons=ingress --cpus=2 --cni=flannel --install-addons=true --kubernetes-version=stable --memory=6g      
  
  
  
 //Run below minikube command to check status,
 
	  ajay@sisaudiya:~$ minikube status
	  minikube
	  type: Control Plane
	  host: Running
	  kubelet: Running
	  apiserver: Running
	  kubeconfig: Configured
	  pkumar@linuxtechi:~$




:end:





<a name="top"></a>
<a name="d_svc_rc"></a>
# Deployment Services(svc) Replicaset(rc)


	microk8s kubectl get all -o wide
        microk8s kubectl get po,svc,deploy

[Go To Top](#top)
<a name="pods"></a>
Pods:

	microk8s kubectl run tif-nginx --image=nginx:alpine --port=80
	microk8s kubectl get pods
	microk8s kubectl get ps -o wide
	microk8s kubectl get pods -o wide
	microk8s kubectl describe pod NAME
	microk8s kubectl describe pod NAME|more
	microk8s kubectl describe pod|more
	microk8s kubectl exec pod_name env
	
	microk8s kubectl describe pod nginx
	microk8s kubectl get pods --all-namespaces
	microk8s kubectl run nginx --image=nginx --restart=Never
	microk8s kubectl delete pod nginx
	microk8s kubectl get pods --show-labels
	microk8s kubectl apply -f abcd.yml --dry-run  //Check yml file is ok or not
	microk8s kubectl create -f abcd.yml
	microk8s kubectl get pod -n test
	
	
	
How to verify 2 containers running in a pod

	microk8s kubectl describe pod
	

In Pod:

	microk8s kubectl exec -it webserver --bash
        microk8s kubectl exec -it webserver -c webwatcher --/bin/bash
	microk8s kubectl exec mc1 -c 1st --/bin /cat/user/share/nginx/html/index.html
	microk8s kubectl exec mc1 -c 2nd --/bin/cat /html/index.html
	
	

[Go To Top](#top)
<a name="deployment"></a>
Devpoyment ():

	microk8s kubectl get deployment  --all-namespaces
	microk8s kubectl explain --recursive deploy
	microk8s kubectl get deployments   //Create deployment
	microk8s kubectl                   //Delete deployment
	microk8s kubectl                   // Listing deployment
	microk8s kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml
	microk8s kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1    //Update Deployment


##Pod's environment and not visible to the outside world.

	microk8s.kubectl expose deployment tjf-nginx --type=NodePort --name=tjf2-nginx




[Go To Top](#top)
<a name="services"></a>
Services (svc):


	microk8s kubectl                   //Create service
	microk8s kubectl                   //Delete service
	microk8s kubectl get svc           //Listing namespace
	microk8s kubectl get svc    	   //Service
	microk8s kubectl get services  --all-namespaces

	servicename.namespacename.svc.cluster.local
	curl myfirstservice.default.svc.cluster.local
	
	
	

[Go To Top](#top)	
<a name="replicas"></a>
ReplicaSet (rc): 

	microk8s kubectl get rc     //Replicaset
	microk8s kubectl get replicasets  --all-namespaces 




[Go To Top](#top)
<a name="namespaces"></a>
NameSpaces (ns): 


	microk8s kubectl create ns test   		//Create namespace
	microk8s kubectl delete ns test  		 //Delete namespace
	microk8s kubectl get ns          		 // Listing namespace
	microk8s kubectl create -f abcd.yml -n test  	 //test namespace
	microk8s kubectl delete ns test   		 //Delete namespace
	microk8s kubectl get all -o wide




[Go To Top](#top)
<a name="nodes"></a>
Nodes: 

##All the nodes are fine. microk8s kubectl get all --all-namespaces

	 microk8s add-node .
	 microk8s inspect
	 microk8s kubectl get node


##Microk8s: how to get the node external-ip, like “minikube ip”? 

	  microk8s.kubectl cluster-info

microk8s.kubectl describe node $(microk8s.kubectl get nodes --no-headers | cut -f 1 -d " ")




##IP address to access my nginx server. I ascertained my nginx IP port by entering 

	microk8s.kubectl get service



        sudo apt install lynx    //After I entered 

	lynx 10.0.0.177:80       // I was presented with the nginx welcome screen
OR
	10.0.0.177:80           //Type on browser (mozilla firefox)





 
##Adding a worker node only with MicroK8s
    .  waiting.....







[Go To Top](#top)
<a name="yml_files"></a>
# 12. Pod yml,deployment yml,service yml file click here


Nodes: 


    1. to create a Node from the following JSON manifest:


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





Pods: 

   1.  pods/simple-pod.yaml:


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


     2. Pod templates:
       

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




       


Deployment: 

   1. Creating a Deployment
      


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
	      


      Command Create Deployment:
      
              kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml
	      
      Update Deployment: 
	      
	      kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1



	or use the following command:

		kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1

	The output is similar to:

	deployment.apps/nginx-deployment image updated

	Alternatively, you can edit the Deployment and change .spec.template.spec.containers[0].image from nginx:1.14.2 to nginx:1.16.1:

		kubectl edit deployment/nginx-deployment

	The output is similar to:

	deployment.apps/nginx-deployment edited

	To see the rollout status, run:

		kubectl rollout status deployment/nginx-deployment

	The output is similar to this:

	Waiting for rollout to finish: 2 out of 3 new replicas have been updated...

	or

	deployment "nginx-deployment" successfully rolled out
	      
	      
	 kubectl get rs
	      
	 kubectl describe deployments
	      
	      
	      
Rolling Back a Deployment:     
	      
	      
	Suppose that you made a typo while updating the Deployment, by putting the image name as nginx:1.161 instead of nginx:1.16.1:

		kubectl set image deployment/nginx-deployment nginx=nginx:1.161 

	The output is similar to this:

	deployment.apps/nginx-deployment image updated

	The rollout gets stuck. You can verify it by checking the rollout status:

		kubectl rollout status deployment/nginx-deployment

	The output is similar to this:

	Waiting for rollout to finish: 1 out of 3 new replicas have been updated.	      

	  
	  kubectl get rs
	  kubectl get pods
	  kubectl describe deployment
	  
	  
Checking Rollout History of a Deployment  

	  kubectl rollout history deployment/nginx-deployment
	  
To see the details of each revision, run:

	  kubectl rollout history deployment/nginx-deployment --revision=2
	  
	
	
Rolling Back to a Previous Revision	  

	Now you've decided to undo the current rollout and rollback to the previous revision:

		kubectl rollout undo deployment/nginx-deployment

	The output is similar to this:

		deployment.apps/nginx-deployment rolled back

	Alternatively, you can rollback to a specific revision by specifying it with --to-revision:

		kubectl rollout undo deployment/nginx-deployment --to-revision=2

	The output is similar to this:

		deployment.apps/nginx-deployment rolled back
	  
	  

		kubectl get deployment nginx-deployment
		kubectl describe deployment nginx-deployment


Scaling a Deployment:

	
	You can scale a Deployment by using the following command:

		kubectl scale deployment/nginx-deployment --replicas=10

	The output is similar to this:

		deployment.apps/nginx-deployment scaled


	to run based on the CPU utilization of your existing Pods.

		kubectl autoscale deployment/nginx-deployment --min=10 --max=15 --cpu-percent=80

	The output is similar to this:

		deployment.apps/nginx-deployment scaled


	
Proportional scaling:


	For example, you are running a Deployment with 10 replicas, maxSurge=3, and maxUnavailable=2.

	    Ensure that the 10 replicas in your Deployment are running.

		 kubectl get deploy

	You update to a new image which happens to be unresolvable from inside the cluster.

		kubectl set image deployment/nginx-deployment nginx=nginx:sometag

	The output is similar to this:

		deployment.apps/nginx-deployment image updated


             kubectl get rs
	     kubectl get deploy
	     kubectl get rs
	     

	
Pausing and Resuming a rollout of a Deployment 


For example, with a Deployment that was created:

Get the Deployment details:

kubectl get deploy

Get the rollout status:

kubectl get rs


Pause by running the following command:

kubectl rollout pause deployment/nginx-deployment


The output is similar to this:

deployment.apps/nginx-deployment paused

Then update the image of the Deployment:

kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1

The output is similar to this:

deployment.apps/nginx-deployment image updated

Notice that no new rollout started:

kubectl rollout history deployment/nginx-deployment

The output is similar to this:

deployments "nginx"
REVISION  CHANGE-CAUSE
1   <none>

Get the rollout status to verify that the existing ReplicaSet has not changed:

kubectl get rs

	
	
You can make as many updates as you wish, for example, update the resources that will be used:

kubectl set resources deployment/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi

The output is similar to this:

deployment.apps/nginx-deployment resource requirements updated
	
	
	
Eventually, resume the Deployment rollout and observe a new ReplicaSet coming up with all the new updates:

kubectl rollout resume deployment/nginx-deployment

The output is similar to this:

deployment.apps/nginx-deployment resumed

Watch the status of the rollout until it's done.

	kubectl get rs -w

Get the status of the latest rollout:

	kubectl get rs
	
	
	
	
#Deployment status:
	
Progressing Deployment:
	
    The Deployment creates a new ReplicaSet.
    The Deployment is scaling up its newest ReplicaSet.
    The Deployment is scaling down its older ReplicaSet(s).
    New Pods become ready or available (ready for at least MinReadySeconds).
	
Complete Deployment
	
	kubectl rollout status deployment/nginx-deployment
	echo $?
	
	
Failed Deployment:
	
	
    Insufficient quota
    Readiness probe failures
    Image pull errors
    Insufficient permissions
    Limit ranges
    Application runtime misconfiguration	
	
	
	kubectl patch deployment/nginx-deployment -p '{"spec":{"progressDeadlineSeconds":600}}'

	
The output is similar to this:

	deployment.apps/nginx-deployment patched
	kubectl describe deployment nginx-deployment
	kubectl get deployment nginx-deployment -o yaml
	kubectl rollout status deployment/nginx-deployment
	echo $?\
	1
	
	
Clean up Policy	
	.spec.revisionHistoryLimit
	
	
	
	

Services:
	
	
Defining a Service:

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


2. 

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
	
	
	
	
	
Replicaset:

1. controllers/frontend.yaml

	apiVersion: apps/v1
	kind: ReplicaSet
	metadata:
	  name: frontend
	  labels:
	    app: guestbook
	    tier: frontend
	spec:
	  # modify replicas according to your case
	  replicas: 3
	  selector:
	    matchLabels:
	      tier: frontend
	  template:
	    metadata:
	      labels:
		tier: frontend
	    spec:
	      containers:
	      - name: php-redis
		image: gcr.io/google_samples/gb-frontend:v3
	
	

	
kubectl apply -f https://kubernetes.io/examples/controllers/frontend.yaml

You can then get the current ReplicaSets deployed:

kubectl get rs

You can also check on the state of the ReplicaSet:

kubectl describe rs/frontend

kubectl get pods
	
kubectl get pods frontend-b2zdv -o yaml
	
	

	apiVersion: v1
	kind: Pod
	metadata:
	  creationTimestamp: "2020-02-12T07:06:16Z"
	  generateName: frontend-
	  labels:
	    tier: frontend
	  name: frontend-b2zdv
	  namespace: default
	  ownerReferences:
	  - apiVersion: apps/v1
	    blockOwnerDeletion: true
	    controller: true
	    kind: ReplicaSet
	    name: frontend
	    uid: f391f6db-bb9b-4c09-ae74-6a1f77f3d5cf
	...	
	
	
	
Non-Template Pod acquisitions:
	
   pods/pod-rs.yaml 
	
	
	apiVersion: v1
	kind: Pod
	metadata:
	  name: pod1
	  labels:
	    tier: frontend
	spec:
	  containers:
	  - name: hello1
	    image: gcr.io/google-samples/hello-app:2.0

	---

	apiVersion: v1
	kind: Pod
	metadata:
	  name: pod2
	  labels:
	    tier: frontend
	spec:
	  containers:
	  - name: hello2
	    image: gcr.io/google-samples/hello-app:1.0	
	
	
kubectl apply -f https://kubernetes.io/examples/pods/pod-rs.yaml
kubectl get pods	
	
If you create the Pods first:

kubectl apply -f https://kubernetes.io/examples/pods/pod-rs.yaml

And then create the ReplicaSet however:

kubectl apply -f https://kubernetes.io/examples/controllers/frontend.yaml
kubectl get pods
	
	
	
	
	
	
	
	


Volumes: 

   
  1 hostPath configuration example
  
  
     Command Create Pod :  kubectl apply -f https://k8s.io/examples/pods/simple-pod.yaml


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

    




  2. EmptyDir configuration example
  
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



       3. AWS EBS configuration example
       
	Before you can use an EBS volume with a pod, you need to create it.

		aws ec2 create-volume --availability-zone=eu-west-1a --size=10 --volume-type=gp2


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




   4. hostPath FileOrCreate configuration example


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



    5. Using subPath


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




   6. Using subPath with expanded environment variables
	

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
	
	
	
	
:end:





[Go To Top](#top)
<a name="error"></a>
Error: 

##The connection to the server 127.0.0.1:16443 was refused - did you specify the right host or port? #1916 


ENV:

host : mac

       multipass ubuntu:20.04 * 2 (one: microk8s-vm-0 the other one: microk8s-vm-1)
       microk8s 1.19/stable


OPERATION:

    multipass shell microk8s-vm-0 and sudo snap install microk8s --classic --channel=1.19/stable

	sudo usermod -a -G microk8s $USER
	sudo chown -f -R $USER ~/.kube

	 microk8s status 
	 microk8s insepct





	DSN - Domain Name Server (Convert hostname to ip)

	


:end:





[Go To Top](#top)
