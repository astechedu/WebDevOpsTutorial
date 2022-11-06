# Kubernetes Commands & Examples For Beginners

## Topics 


###### Basic Commands [Go to Basic Commands](#basic_commands)

##### Minikube [Go to Minikube](#minikube)

##### KubeCTL [Go to Kubectl](#kubectl)

##### Create YML File [Go to Create YML File](#create_yml_file)

##### Microk8s CMDS [Go to Microk8s](#micro8ks_cmds)

	

<!----><a name="basic_commands">Go Top</a>
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
	   
     	   
## Minikube & KubeCTL

	What is Minikube
	Minikube installation steps in windows
	How to deploy first spring boot application to Kubernetes


Installatioin: 

	1. Minikube     (  )
	2. KubeCTL      (  )

Requirements:

	  1. Virtual Box Or Hiper-V or docker ( as a driver )


<!----><a name="minikube"></a>

### 1. Minikube Installation ( minikube.exe )

	   Usually used to run k8s cluster in your local machine/computer.
	   Minikube runs a single-node Kubernetes cluster on your machine so that you can try out Kubernetes for your daily development work.
	   Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one  node.
	   
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
 
 
<!----><a name="micro8ks_cmds">Top</a>

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

--------------------------------------------

