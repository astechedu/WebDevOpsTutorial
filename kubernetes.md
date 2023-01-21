<!-- # Kubernetes Commands & Examples For Beginners -->
$$\large{\colorbox{black}{\color{white}Kubernetes \ Commands \ and \ Examples \ For \ Beginners}}$$

:link:[Home](all-file-links.md)     

<!--$\color{blue}ajay$-->
<!--Minikube:-->

<a name="top"></a>
[Go To Bottom](#bottom)
## Topics 

###### 1. Basic Commands [Go to Basic Commands click here](#basic_commands)
###### 2. Minikube [Go to Minikube click here](#minikube)
###### 3. KubeCTL [Go to Kubectl click here](#kubectl)
###### 4. Create YML File [Go to Create YML File click here](#create_yml_file)
###### 5. Microk8s CMDS [Go to Microk8s click here](#micro8ks_cmds)
###### 5. Microk8s CMDS [Go to Installation Minikube on Ubuntu click here](#install_minikube)
###### 6. Microk8s CMDS [Go To Nodes on Ubuntu click here](#nodes)  
###### 7. Microk8s CMDS [Go To Installation Local Kubernetes for Linux – MiniKube vs MicroK8s click here](#k8-on-local)
###### 8. Microk8s CMDS [Go To Namespaces(nc) on Ubuntu click here](#namespaces)
###### 9. Microk8s CMDS [Go To Pods(po) on Ubuntu click here](#pods)
###### 10. Microk8s CMDS [Go To Deployment(deploy) on Ubuntu click here](#deployment)
###### 11. Microk8s CMDS [Go To Services(svc) on Ubuntu click here](#services)
###### 12. Microk8s CMDS [Go To Replicas(rc) on Ubuntu click here](#replicas)
###### 13 Microk8s CMDS [Go To Ingress on Ubuntu click here](#ingress)

###### 14 Microk8s CMDS [Node yml file click here](#yml_nodes)
###### 15 Microk8s CMDS [Pod yml file click here](#yml_pods)
###### 16 Microk8s CMDS [Deployment yml click here](#yml_deployments)
###### 17 Microk8s CMDS [Service yml file click here](#yml_services)
###### 18 Microk8s CMDS [Replicaset yml file click here](#yml_replicasets)
###### 19 Microk8s CMDS [Namespaces yml file click here](#yml_namespaces)
###### 20 Microk8s CMDS [Ingress yml file click here](#yml_ingress)

###### 21 crok8s CMDS [The connection to the server 127.0.0.1:16443 was refused - did you specify the right host or port? on Ubuntu click here](#replicas)

###### 22 Microk8s CMDS [First App click here](#k-first-app)

###### 23 Microk8s CMDS [Deploy and Access the Kubernetes Dashboard](#k8-dashboard)




[Go To Top](#top)
<!----><a name="basic_commands"></a>

$\large{\color{blue} \ Basic \ Commands}$



$\color{green}0. \ Display \ all \ list \ (pods, \ services, \ deployments \ and \ riplicaSets)$
	
	   kubectl get all --all-namespaces  
	   microk8s enable dns storage           //Use add-ons



$\color{green}1. \ Run \ a \ yamal \ file$

	   //Output redirect to new yaml file
	   kubectl run secondpod --dry-run --generator=run-pod/v1 --image=astechutube/nginx-custom -o yaml > mysecondpd.yml

	   kubectl create -f firstpod.yml --dry-run
	   kubectl apply -f firstpod.yml
	   cat myfirstpod.yml
	   kubectl create -f firstpod.yml

$\color{green}2. \ Pods$
           
	   kubectl get pods
	   kubectl delete pod myfirstpod
	   kubectl explain pod --recursive !less
           	   
	   kubectl run secondpod --generator=run-pod/v1 --image=astechutube/nginx-custom
	   //Client side run 
	   kubectl run secondpod --dry-run --generator=run-pod/v1 --image=astechutube/nginx-custom
	   kubectl run secondpod --dry-run --generator=run-pod/v1 --image=astechutube/nginx-custom -o yaml
           

$\color{green}3. \ Services$

	   kubectl get services

$\color{green}4. \ Deployment$

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

$\large{\color{blue} \ Minikube \ and \ KubeCTL}$


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

$\large{\color{blue} \ Minikube \ Installation ( minikube.exe )}$

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
	    image: astechutube/nginx-custom


	 Run Yamal File: 
	 kubectl create -f firstpod.yml --dry-run
	 cat myfirstpod.yml
	 kubectl create -f firstpod.yml
	 kubectl get pods
	 kubectl explain pod --recursive !less


#basic-commands
This is heading 


 //Create k8s pod
 
	 kubectl run secondpod --generator=run-pod/v1 --image=astechutube/nginx-custom
	 //Client side run 
	 kubectl run secondpod --dry-run --generator=run-pod/v1 --image=astechutube/nginx-custom
	 kubectl run secondpod --dry-run --generator=run-pod/v1 --image=astechutube/nginx-custom -o yaml

 //Output redirect to new yaml file
 
  	kubectl run secondpod --dry-run --generator=run-pod/v1 --image=astechutube/nginx-custom -o yaml > mysecondpd.yml
    
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
	kubectl logs <podName> --all-containers
	kubectl logs <podName> -c <containerName>

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
	    image: astechutube/nginx-custom
	    env:
	     - name: myname
	       value: Gaurav
	     - name: City
	       value: Jaipur
	    args: ["sleep","3600"]
	  - name: secondcontainer
	    image: astechutube/nginx-custom  

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
	
	minikube service <service-name> --url 
	
	

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









# 12. Pod yml,deployment yml,service yml file click here


[Go to Top](#top)
<a name="yml_nodes"></a>
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




[Go to Top](#top)
<a name="yml_pods"></a>
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


     2.
	apiVersion: v1
	kind: Pod
	metadata:
	  name: nginx
	  labels:
	    env: dev
	spec:
	  containers:
	  - name: nginx
	    image: nginx:1.14.2
	    ports:
	    - containerPort: 80
	    

     3.
	apiVersion: v1
	kind: Pod
	metadata:
	  name: nginx
	  labels:
	    env: dev
	spec:
	  containers:
	  - name: nginx
	    image: nginx:1.14.2
	    ports:
	    - containerPort: 80
	    env: 
	     - name: myname
	       value: ajay
	     - name: city
	       value: Dehradun
	    
	    

     4.
	apiVersion: v1
	kind: Pod
	metadata:
	  name: nginx
	spec:
	  containers:
	  - name: server1
	    image: nginx:1.14.2    
	  - name: server2
	    image: nginx:1.14.2


     5.
	apiVersion: v1
	kind: Pod
	metadata:
	  name: nginx
	spec:
	  containers:
	  - name: server1
	    image: nginx:1.14.2
	    ports:
	    - containerPort: 80
	  - name: server2
	    image: nginx:1.14.2
	    ports:
	    - containerPort: 80
	    	    
	    
	    
     6. Pod templates:
       

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



    7. Volumes: 
    
	apiVersion: v1
	kind: Pod
	metadata:
	  name: textvols2
	spec:
	  containers:
	   - name: server2
	     image: nginx

	     volumeMounts:
	      - name: txtvols
		#mountPath: /data
		mountPath: /usr/share/nginx/html

	  volumes:
	   - name: txtvols
	     hostPath:
	      # directory location on host
	      path: /tmp/data
	      # this field is optional
	      type: Directory



       

[Go to Top](#top)
<a name="yml_deployments"></a>
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
	
	
	

	
[Go to Top](#top)
<a name="yml_services"></a>
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
	
	
	
	
	
	
	
[Go To Top](#top)	
<a name="yml_replicasets"></a>	
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
	
	
	
	
	
	
	
	
[Go To Top](#top)	
<a name="yml_volumes"></a>
Volumes: 

   
1. Empty Directory:

	apiVersion: v1
	kind: pod
	metadata:
	  name: test-vol
	spec:
	  containers:
	  - image: myimg/name
	    name: text-container
	    volumeMounts: 
	    - mountPath: /data
	      name: first-volume
	   volumes: 
	   - name: first-volume
	     emptyDir: {}   



2. Host Path

	apiVersion: v1
	kind: pod
	metadata:
	  name: test-vol
	spec:
	  containers:
	  - image: myimg/name
	    name: text-container
	    volumeMounts: 
	     - mountPath: /data
	      name: first-volume
	   volumes: 
	   - name: first-volume
	     hostPath: 
	      path: /tmp/data







  3 hostPath configuration example
  
  
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

    




  4. EmptyDir configuration example
  
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



       5. AWS EBS configuration example
       
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




   6. hostPath FileOrCreate configuration example


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



    7. Using subPath


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




   8. Using subPath with expanded environment variables
	

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
	

	
	
	
	
[Go To Top](#top)
<a name="yml_namespaces"></a>
NameSpaces:
	
    Create a new Kubernetes namespace:
	
	kubectl create namespace <name>
	
	
	
my-namespace.yaml:


	apiVersion: v1
	kind: Namespace
	metadata:
	  name: <insert-namespace-name-here>

	Then run:

	kubectl create -f my-namespace.yaml

	The command to display all namespaces in the cluster is:

	kubectl get namespace	
	
	
 How to switch between Kubernetes namespaces?

	kubectl config set-context –current –namespace=K21


 How to delete a Kubernetes namespace?


 Delete a namespace with the below command:


	kubectl delete namespaces <name>


	
:end:




[Go To Top](#top)
<a name="ingress"></a>
# Ingress








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
<a name="k-first-app"></a>
# Kubernetes First App


Step 1:

Docker: 

  Creating docker image:


   Dockerfile:
   
	FROM node:7
	ADD app.js /app.js
	ENTRYPOINT ["node","app.js"]



	dockercontainer# ps aux

	sudo ps aux | grep app.js

	sudo docker tag kubia img/name  //Same img diff tag

	sudo docker images | head

	sudo docker login -u abc -p 


  app.js
 
	<code>
	var http = require('http');

	//create a server object:
	http.createServer(function (req, res) {
	  res.write('Hello World!'); //write a response to the client
	  res.end(); //end the response
	}).listen(8080); //the server object listens on port 8080 
	</code>



Step: 2

 Kubernetes: 


Creating First App:

	sudo kubectl create deployment --image img/name kubia  
	sudo kubectl scale deployment kubia --replicas 3
	sudo kubectl expose deployment kubia --type=NodePort --port 8080

	sudo kubectl get pods
	sudo kubectl get services





:end:

















[G0 To Top](#top)
<a name="k8-on-local"></a>
	
$\large{\color{blue}7. \ Installation \ Local \ Kubernetes \ for \ Linux \ – \ MiniKube \ vs \ MicroK8s}$


$\large{\colorbox{black}{\color{yellow}Minikube:}}$

Minikube runs a single-node Kubernetes cluster inside a VM (e.g. Virtualbox ) in your local development environment. The result is a local Kubernetes endpoint that you can use with the kubectl client. Minikube supports most typical Kubernetes features such as DNS, Dashboards, CNI, NodePorts, Config Maps, etc. . It also supports multiple hypervisors, such as Virtualbox, kvm, etc.



##### Installation:

In order to install Minikube to Linux, you can follow the steps described in the official documentation. In our evaluation we used Ubuntu 18.04 LTS with VirtualBox support using the following commands:

	sudo apt install virtualbox virtualbox-ext-pack //vbox requirements
	wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
	chmod +x minikube-linux-amd64
	sudo mv minikube-linux-amd64 /usr/local/bin/minikube

After installation of Minikube, the kubectl
tool needs to be installed in order to deploy and manage applications on Kubernetes. You can install kubectl
by adding a new APT repository using the following command:

	curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
	echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
	sudo apt update
	sudo apt install kubectl

Finally, after successful installation, you can start your minikube by issuing the command:
minikube start 


###### Management and Deployment

Managing a Minukube cluster on Linux is exactly the same as managing it on Windows.



$\large{\colorbox{black}{\color{yellow}Microk8s:}}$

Microk8s is a new solution for running a lightweight Kubernetes local cluster. It was developed by the Kubernetes team at Canonical. It is designed to be a fast and lightweight upstream Kubernetes installation isolated from your local environment. This isolation is achieved by packaging all the binaries for Kubernetes, Docker.io, iptables, and CNI in a single snap package (available only in Ubuntu and compatible distributions).

By installing Microk8s using snap, you are able to create a “clean” deploy of the latest upstream Kubernetes on your local machine without any other overhead. The Snap tool is taking care of all needed operations and can upgrade all associated binaries to their latest versions. By default, Microk8s installs and runs the following services:

    Api-server
    Controller-manager
    scheduler
    kubelet
    cni

Additional services such as the Kubernetes dashboard can be easily enabled/disabled using the microk8s.enable
and microk8s.disable
command. The list of available services are:

    Dns
    Dashboard, including grafana and influxdb
    Storage
    Ingress, Istio
    Registry
    Metrics Server


##### Installation

Microk8s can be installed as a single snap command, directly from the Snap store.

	sudo snap install microk8s --classic

This will install the microk8s
command and an api-server, controller-manager, scheduler, etcd, kubelet, cni, kube-proxy, and Docker. To avoid any conflicts with existing installation of Kubernetes, Microk8s adds a microk8s.kubectl
command, configured to exclusively access the new Microk8s install. When following any generic Kubernetes instructions online, make sure to prefix kubectl
with Microk8s. To verify that installation was successful, you can use the following commands to retrieve available nodes and available services respectively:

	microk8s.kubectl get nodes
	microk8s.kubectl get services
	
	
###### Management

As mentioned above, Microk8s installs a barebones upstream Kubernetes. This means just the api-server, controller-manager, scheduler, kubelet, cni, and kube-proxy are installed and run. Additional services such as kube-dns and the dashboard can be run using the microk8s.enable command.
microk8s.enable dns dashboard

You can verify that all services are up and running with the following command:

	pliakas@zouzou:~$ microk8s.kubectl get all --all-namespaces

	NAMESPACE     NAME                                                  READY     STATUS    RESTARTS   AGE
	kube-system   pod/heapster-v1.5.2-84f5c8795f-n8dmd                  4/4       Running   8          11h
	kube-system   pod/kube-dns-864b8bdc77-8d8lk                         2/3       Running   191        11h
	kube-system   pod/kubernetes-dashboard-6948bdb78-z4knb              1/1       Running   97         11h
	kube-system   pod/monitoring-influxdb-grafana-v4-7ffdc569b8-g6nrv   2/2       Running   4          11h


	NAMESPACE     NAME                           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
	default       service/kubernetes             ClusterIP   10.152.183.1             443/TCP             12h
	kube-system   service/heapster               ClusterIP   10.152.183.58            80/TCP              11h
	kube-system   service/kube-dns               ClusterIP   10.152.183.10            53/UDP,53/TCP       11h
	kube-system   service/kubernetes-dashboard   ClusterIP   10.152.183.77            443/TCP             11h
	kube-system   service/monitoring-grafana     ClusterIP   10.152.183.253           80/TCP              11h
	kube-system   service/monitoring-influxdb    ClusterIP   10.152.183.15            8083/TCP,8086/TCP   11h


	NAMESPACE     NAME                                             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
	kube-system   deployment.apps/heapster-v1.5.2                  1         1         1            1           11h
	kube-system   deployment.apps/kube-dns                         1         1         1            0           11h
	kube-system   deployment.apps/kubernetes-dashboard             1         1         1            1           11h
	kube-system   deployment.apps/monitoring-influxdb-grafana-v4   1         1         1            1           11h


	NAMESPACE     NAME                                                        DESIRED   CURRENT   READY     AGE
	kube-system   replicaset.apps/heapster-v1.5.2-84f5c8795f                  1         1         1         11h
	kube-system   replicaset.apps/kube-dns-864b8bdc77                         1         1         0         11h
	kube-system   replicaset.apps/kubernetes-dashboard-6948bdb78              1         1         1         11h
	kube-system   replicaset.apps/monitoring-influxdb-grafana-v4-7ffdc569b8   1         1         1         11h

You can access any service by pointing the correct CLUSTER_IP
to your browser. For example, you can access the dashboard by using the following web address, https://10.152.183.77. See image below for the dashboard:


###### Kubernetes dashboard

At any time, you can pause and restart all Kubernetes services and installed containers without losing any of your configurations by issuing the following command. (Note that this will also disable all commands prefixed with Microk8s.)
snap disable microk8s

Removing Microk8s is very easy. You can do so by first disabling all Kubernetes services and then using the snap command to remove the complete installation and configuration files.
microk8s.disable dashboard dns
sudo snap remove microk8s


###### Deployment

Deploying a nginx service is what you would expect, with the addition of the Microk8s prefix:

	microk8s.kubectl run nginx --image nginx --replicas 3
	microk8s.kubectl expose deployment nginx --port 80 --target-port 80 --type ClusterIP\ --selector=run=nginx --name nginx

You can monitor your deployed services using the command:

	pliakas@zouzou:~$ microk8s.kubectl get all
	

	NAME                         READY     STATUS    RESTARTS   AGE
	
	pod/nginx-64f497f8fd-86xlj   1/1       Running   0          2m
	pod/nginx-64f497f8fd-976c4   1/1       Running   0          2m
	pod/nginx-64f497f8fd-r2tsv   1/1       Running   0          2m
	
	NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
	service/kubernetes   ClusterIP   10.152.183.1             443/TCP   13h
	service/nginx        ClusterIP   10.152.183.125           80/TCP    1m
	
	NAME                    DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
	deployment.apps/nginx   3         3         3            3           2m
	
	NAME                               DESIRED   CURRENT   READY     AGE
	replicaset.apps/nginx-64f497f8fd   3         3         3         2m

Now you are ready to access your deployed web service by pointing the following web url to your preferred web browser: http://10.152.183.125


:end:




<a name="k8-dashboard"></a>
# Deploy and Access the Kubernetes Dashboard


Deploying the Dashboard UI:

	microk8s enable dashboard
	microk8s kubectl create token default
 
 
 kubernetes-dashboard   service/kubernetes-dashboard   ClusterIP   10.152.183.51   <none>   443/TCP  37m

	On Browser: 
	
	 https://ip:port
	
	 https://10.152.183.51:443


	On Borwser (UI):
	
	 login: Paste toke here
	
	
	
OR	

Deploying the Dashboard UI:

The Dashboard UI is not deployed by default. To deploy it, run the following command:

	kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml



Accessing the Dashboard UI:


Command line proxy

You can enable access to the Dashboard using the kubectl command-line tool, by running the following command:

        kubectl proxy --help
	kubectl proxy










[Go To Top](#top)
<a name="bottom"></a>
