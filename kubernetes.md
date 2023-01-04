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
  
###### 6. Microk8s CMDS [Go To Deployment Services(svc) Replicas(rc) on Ubuntu click here](#d_svc_rc)
  
	


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

Devpoyment ():


	microk8s kubectl get deployments   //Create deployment
	microk8s kubectl                   //Delete deployment
	microk8s kubectl                   // Listing deployment
	microk8s kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml
	microk8s kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1    //Update Deployment


##Pod's environment and not visible to the outside world.

	microk8s.kubectl expose deployment tjf-nginx --type=NodePort --name=tjf2-nginx



Services (svc):


	microk8s kubectl                   //Create service
	microk8s kubectl                   //Delete service
	microk8s kubectl get svc           //Listing namespace



ReplicaSet (rc): 

	microk8s kubectl get rc     //Replicaset



Name Space (ns): 


	microk8s kubectl create ns test   //Create namespace
	microk8s kubectl delete ns test   //Delete namespace
	microk8s kubectl get ns           // Listing namespace




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





microk8s: 
 //Single line commands
 
//Creating a pod
microk8s kubectl run tif-nginx --image=nginx:alpine --port=80
microk8s kubectl get pods
microk8s kubectl get pods -o wide
microk8s kubectl describe pod NAME

microk8s kubectl exec pod_name  env

microk8s kubectl get pods --all-namespaces
microk8s kubectl get deployment  --all-namespaces
microk8s kubectl get services  --all-namespaces
microk8s kubectl get replicasets  --all-namespaces
microk8s kubectl describe pod nginx
 
microk8s kubectl run nginx --image=nginx --restart=Never
microk8s kubectl delete pod nginx
microk8s kubectl delete ns test   //Delete namespace
microk8s kubectl get all -o wide
microk8s kubectl get pods --show-labels
microk8s kubectl apply -f abcd.yml --dry-run  //Check yml file is ok or not
microk8s kubectl create -f abcd.yml
microk8s kubectl create -f abcd.yml -n test   //test namespace
microk8s kubectl get pod -n test

microk8s kubectl explain --recursive deploy

microk8s kubectl get ns     //namespace
microk8s kubectl get svc    //Service
microk8s kubectl get rc     //Replica

microk8s kubectl exec -it webserver --bash

DSN - Domain Name Server (Convert hostname to ip)


servicename.namespacename.svc.cluster.local

curl myfirstservice.default.svc.cluster.local


:end:





[Go To Top](#top)
