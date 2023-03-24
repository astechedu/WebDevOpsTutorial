
$$\large{\color{purple} Interview \ Questions \ And \ Answers}$$ <br />

$\large{\color{green} Ajay \ Sisaudiya }$

[Home](#all-file-links.md)

<a name="top"></a>    

Topics:

[Kubernetes Top 10 Questions Answers](#kubernetes-Q-A-1)
[Kubernetes Top 50 Question Answers](#kubernetes-Q-A-2)
[PHP Interview Questions And Answers For 5 Year Experience](#php5years-Q-A-2)





#

[Top](#top)
<a name="kubernetes-Q-A-1"></a>

# Kubernetes Top 10 Questions and Answers


Top 10 Kubernetes Related Interview Questions:

1. Kubernetes Architecture? (MasterNode/WorkerNode/KubApi/Etcd/Scheduler/Controller/Kubelet/kube-proxy)
2. Replication Controller vs Replica Set Controller
3. Stateless vs Statefull Deployment In kubernetes
4. Storage Class
5. There is an pod and Node which showing in pending state? reason?
6. What is advantage of Calico Network in kubernetes and traffic flow
7. Sidecar container and Init Container and Daemon Set based Deployment?
8. User role access concept
9. Ingress Controller concept how it works
10. Network security between the Pod Communication





#
[Top](#top)
<a name="kubernetes-Q-A-2"></a>

# Top 50 Kubernetes Interview Questions and Answers

1. How is Kubernetes different from Docker Swarm?
2. What is Kubernetes?
3. How is Kubernetes related to Docker?
4. What is the difference between deplying applications on hosts and containers?
5. What is Container Orchestrtion?
6. What is the need for Container Orchestration?
7. What are the features of Kubernetes
8. How does Kubernetes simplify containerized Deployment?
9. What do you know about clusters in Kubernetes?
10. What is Google Container Engine?


* Kubernetes Basic Interview Questions
* Architecture-Based Interview Questions
* Scenario-Based Interview Questions
* Multiple Choice Questions
    
    
    
Basic Kubernetes Interview Questions: 

Q1. How is Kubernetes different from Docker Swarm?

    
Features	Kubernetes	Docker Swarm
Installation & Cluster Config	Setup is very complicated, but once installed cluster is robust.	Installation is very simple, but the cluster is not robust.
GUI	GUI is the Kubernetes Dashboard.	There is no GUI.
Scalability	Highly scalable and scales fast.	Highly scalable and scales 5x faster than Kubernetes.
Auto-scaling	Kubernetes can do auto-scaling.	Docker swarm cannot do auto-scaling.
Load Balancing	Manual intervention needed for load balancing traffic between different containers and pods.	Docker swarm does auto load balancing of traffic between containers in the cluster.
Rolling Updates & Rollbacks	Can deploy rolling updates and does automatic rollbacks.	Can deploy rolling updates, but not automatic rollback.
DATA Volumes	Can share storage volumes only with the other containers in the same pod.	Can share storage volumes with any other container.
Logging & Monitoring	In-built tools for logging and monitoring.	3rd party tools like ELK stack should be used for logging and monitoring.

#
Q2. What is Kubernetes?

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/q1-1.png" width=25%>

Kubernetes is an open-source container management tool that holds the responsibilities of container deployment, scaling & descaling of containers & load balancing. Being Google’s brainchild, it offers excellent community and works brilliantly with all the cloud providers. So, we can say that Kubernetes is not a containerization platform, but it is a multi-container management solution. 

#
Q3. How is Kubernetes related to Docker?

It’s a known fact that Docker provides the lifecycle management of containers and a Docker image builds the runtime containers. But, since these individual containers have to communicate, Kubernetes is used. So, Docker builds the containers and these containers communicate with each other via Kubernetes. So, containers running on multiple hosts can be manually linked and orchestrated using Kubernetes.

#
Q4. What is the difference between deploying applications on hosts and containers?

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/Application-768x472.png" width=35%>

Deploying Applications On Host vs Containers:


Refer to the above diagram. The left side architecture represents deploying applications on hosts. So, this kind of architecture will have an operating system and then the operating system will have a kernel that will have various libraries installed on the operating system needed for the application. So, in this kind of framework you can have n number of applications and all the applications will share the libraries present in that operating system whereas while deploying applications in containers the architecture is a little different.

This kind of architecture will have a kernel and that is the only thing that’s going to be the only thing common between all the applications. So, if there’s a particular application that needs Java then that particular application we’ll get access to Java and if there’s another application that needs Python then only that particular application will have access to Python.

The individual blocks that you can see on the right side of the diagram are basically containerized and these are isolated from other applications. So, the applications have the necessary libraries and binaries isolated from the rest of the system, and cannot be encroached by any other application.

#

Q5. What is Container Orchestration?

Consider a scenario where you have 5-6 microservices for an application. Now, these microservices are put in individual containers, but won’t be able to communicate without container orchestration. So, as orchestration means the amalgamation of all instruments playing together in harmony in music, similarly container orchestration means all the services in individual containers working together to fulfill the needs of a single server.


#
Q6. What is the need for Container Orchestration?

Consider you have 5-6 microservices for a single application performing various tasks, and all these microservices are put inside containers. Now, to make sure that these containers communicate with each other we need container orchestration.

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/5-1.png" width=40%>

Challenges Without Container Orchestration

As you can see in the above diagram, there were also many challenges that came into place without the use of container orchestration. So, to overcome these challenges the container orchestration came into place.


#
Q7. What are the features of Kubernetes?

The features of Kubernetes, are as follows:

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/7.png" width=40%>


#
Q8. How does Kubernetes simplify containerized Deployment?

As a typical application would have a cluster of containers running across multiple hosts, all these containers would need to talk to each other. So, to do this you need something big that would load balance, scale & monitor the containers. Since Kubernetes is cloud-agnostic and can run on any public/private providers it must be your choice simplify containerized deployment.

#
Q9. What do you know about clusters in Kubernetes?

The fundamental behind Kubernetes is that we can enforce the desired state management, by which I mean that we can feed the cluster services of a specific configuration, and it will be up to the cluster services to go out and run that configuration in the infrastructure.


<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/Containers-1.png" width=35%>

Representation Of Kubernetes Cluster 

So, as you can see in the above diagram, the deployment file will have all the configurations required to be fed into the cluster services. Now, the deployment file will be fed to the API and then it will be up to the cluster services to figure out how to schedule these pods in the environment and make sure that the right number of pods are running.

So, the API which sits in front of services, the worker nodes & the Kubelet process that the nodes run, all together make up the Kubernetes Cluster.


#

Q10. What is Google Container Engine?

Google Container Engine (GKE) is an open-source management platform for Docker containers and clusters. This Kubernetes based engine supports only those clusters which run within Google’s public cloud services.


#
Q11.  What is Heapster?

Heapster is a cluster-wide aggregator of data provided by Kubelet running on each node. This container management tool is supported natively on Kubernetes cluster and runs as a pod, just like any other pod in the cluster. So, it basically discovers all nodes in the cluster and queries usage information from the Kubernetes nodes in the cluster, via on-machine Kubernetes agent.
Q12.  What is Minikube?

Minikube is a tool that makes it easy to run Kubernetes locally. This runs a single-node Kubernetes cluster inside a virtual machine.

#
Q13.  What is Kubectl?

Kubectl is the platform using which you can pass commands to the cluster. So, it basically provides the CLI to run commands against the Kubernetes cluster with various ways to create and manage the Kubernetes component.

#
Q14.  What is Kubelet?

This is an agent service which runs on each node and enables the slave to communicate with the master. So, Kubelet works on the description of containers provided to it in the PodSpec and makes sure that the containers described in the PodSpec are healthy and running.


#
Q15. What do you understand by a node in Kubernetes?

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/15-1.png" width=50%>


Node In Kubernetes 


#
Architecture-Based Kubernetes Interview Questions

This section of questions will deal with the questions related to the architecture of Kubernetes.

#
Q1. What are the different components of Kubernetes Architecture?

The Kubernetes Architecture has mainly 2 components – the master node and the worker node. As you can see in the below diagram, the master and the worker nodes have many inbuilt components within them. The master node has the kube-controller-manager, kube-apiserver, kube-scheduler, etcd. Whereas the worker node has kubelet and kube-proxy running on each node.



<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/16-1.png" width=50%>

Architecture Of Kubernetes

#

Q2. What do you understand by Kube-proxy?

Kube-proxy can run on each and every node and can do simple TCP/UDP packet forwarding across backend network service. So basically, it is a network proxy that reflects the services as configured in Kubernetes API on each node. So, the Docker-linkable compatible environment variables provide the cluster IPs and ports which are opened by proxy.


#
Q3.  Can you brief on the working of the master node in Kubernetes?

Kubernetes master controls the nodes and inside the nodes the containers are present. Now, these individual containers are contained inside pods and inside each pod, you can have a various number of containers based upon the configuration and requirements. So, if the pods have to be deployed, then they can either be deployed using user interface or command-line interface. Then, these pods are scheduled on the nodes, and based on the resource requirements, the pods are allocated to these nodes. The kube-apiserver makes sure that there is communication established between the Kubernetes node and the master components.



<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/18-1.png" width=35%>

Representation Of Kubernetes Master Node


#
Q4.  What is the role of kube-apiserver and kube-scheduler?

The kube – apiserver follows the scale-out architecture and is the front end of the master node control panel. This exposes all the APIs of the Kubernetes Master node components and is responsible for establishing communication between Kubernetes Node and the Kubernetes master components.

The kube-scheduler is responsible for distributing and managing the workload on the worker nodes. So, it selects the most suitable node to run the unscheduled pod based on resource requirements and keeps track of resource utilization. It ensures that the workload is not scheduled on already full nodes.



#
Q5.  Can you brief me about the Kubernetes controller manager?

Multiple controller processes run on the master node but are compiled together to run as a single process: the Kubernetes Controller Manager. So, Controller Manager is a daemon that embeds controllers and does namespace creation and garbage collection. It owns the responsibility and communicates with the API server to manage the end-points.

So, the different types of controller manager running on the master node are :
Types Of Controllers - Kubernetes Interview Questions - Edureka


<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/25-1.png" width=35%>

Types Of Controllers

#

Q6.  What is ETCD?

Etcd is written in Go programming language and is a distributed key-value store used for coordinating distributed work. So, Etcd stores the configuration data of the Kubernetes cluster, representing the state of the cluster at any given point in time.

#
Q7. What are the different types of services in Kubernetes? 

The following are the different types of services used:

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/22-1.png" width=35%>

Types Of Services


#
Q8. What do you understand by load balancer in Kubernetes?

A load balancer is one of the most common and standard ways of exposing service. There are two types of load balancer used based on the working environment i.e. either the Internal Load Balancer or the External Load Balancer. The Internal Load Balancer automatically balances load and allocates the pods with the required configuration whereas the External Load Balancer directs the traffic from the external load to the backend pods.
Kubernetes Interview Questions


#


Kubernetes Interview Questions


#
Q9. What is Ingress network, and how does it work?

Ingress network is a collection of rules that acts as an entry point to the Kubernetes cluster. This allows inbound connections, which can be configured to give services externally through reachable URLs, load balance traffic, or by offering name-based virtual hosting. So, Ingress is an API object that manages external access to the services in a cluster, usually by HTTP and is the most powerful way of exposing service.

Now, let me explain to you the working of Ingress network with an example.

There are 2 nodes having the pod and root network namespaces with a Linux bridge. In addition to this, there is also a new virtual ethernet device called flannel0(network plugin) added to the root network.


Now, suppose we want the packet to flow from pod1 to pod 4. Refer to the below diagram.

Ingress Network


<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/Pods.png" width=35%>

    
 Working Of Ingress Network
 
 
 

    So, the packet leaves pod1’s network at eth0 and enters the root network at veth0.
    Then it is passed on to cbr0, which makes the ARP request to find the destination and it is found out that nobody on this node has the destination IP address.
    So, the bridge sends the packet to flannel0 as the node’s route table is configured with flannel0.
    Now, the flannel daemon talks to the API server of Kubernetes to know all the pod IPs and their respective nodes to create mappings for pods IPs to node IPs.
    The network plugin wraps this packet in a UDP packet with extra headers changing the source and destination IP’s to their respective nodes and sends this packet out via eth0.
    Now, since the route table already knows how to route traffic between nodes, it sends the packet to the destination node2.
    The packet arrives at eth0 of node2 and goes back to flannel0 to de-capsulate and emits it back in the root network namespace.
    Again, the packet is forwarded to the Linux bridge to make an ARP request to find out the IP that belongs to veth1.
    The packet finally crosses the root network and reaches the destination Pod4. 
     
    
    
#
Q10.  What do you understand by Cloud controller manager?

The Cloud Controller Manager is responsible for persistent storage, network routing, abstracting the cloud-specific code from the core Kubernetes specific code, and managing the communication with the underlying cloud services. It might be split out into several different containers depending on which cloud platform you are running on and then it enables the cloud vendors and Kubernetes code to be developed without any inter-dependency. So, the cloud vendor develops their code and connects with the Kubernetes cloud-controller-manager while running the Kubernetes.

The various types of cloud controller manager are as follows:

Types of Cloud Controller Manager



<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/20-2.png" width=35%>
   
      
Types Of Cloud Controller Manager    
    
#
    
Q11. What is Container resource monitoring?

As for users, it is really important to understand the performance of the application and resource utilization at all the different abstraction layer, Kubernetes factored the management of the cluster by creating abstraction at different levels like container, pods, services and whole cluster. Now, each level can be monitored and this is nothing but Container resource monitoring.

The various container resource monitoring tools are as follows:

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/26.png" width=35%>
          


Container Resource Monitoring Tools

    
#

Q12. What is the difference between a replica set and a replication controller?

Replica Set and Replication Controller do almost the same thing. Both ensure that a specified number of pod replicas are running at any given time. The difference comes with the usage of selectors to replicate pods. Replica Set uses Set-Based selectors while replication controllers use Equity-Based selectors.

    Equity-Based Selectors: This type of selector allows filtering by label key and values. So, in layman’s terms, the equity-based selector will only look for the pods with the exact same phrase as the label.
    
    Example: Suppose your label key says app=nginx; then, with this selector, you can only look for those pods with label app equal to nginx.
    Selector-Based Selectors: This type of selector allows filtering keys according to a set of values. So, in other words, the selector-based selector will look for pods whose label has been mentioned in the set.
    
    Example: Say your label key says app in (Nginx, NPS, Apache). Then, with this selector, if your app is equal to any of Nginx, NPS, or Apache, the selector will take it as a true result.    
    
    
#
Q13. What is a Headless Service?

Headless Service is similar to that of a ‘Normal’ service but does not have a Cluster IP. This service enables you to directly reach the pods without the need to access them through a proxy.


#

Q14. What are the best security measures that you can take while using Kubernetes?

The following are the best security measures that you can follow while using Kubernetes:


Security Measures


<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/26.png" width=35%>
   


Best Security Mesures


#
Q15. What are federated clusters?

Multiple Kubernetes clusters can be managed as a single cluster with the help of federated clusters. So, you can create multiple Kubernetes clusters within a data center/cloud and use federation to control/manage them all at one place.


The federated clusters can achieve this by doing the following two things. Refer to the below diagram.


<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/08/30.png" width=35%>
  
Federated Clusters


#
***Scenario-Based Interview Questions***

Scenario 1: Suppose a company built on monolithic architecture handles numerous products. Now, as the company expands in today’s scaling industry, their monolithic architecture started causing problems.

How do you think the company shifted from monolithic to microservices and deploy their services containers?

Solution:

As the company’s goal is to shift from their monolithic application to microservices, they can end up building piece by piece, in parallel and just switch configurations in the background. Then they can put each of these built-in microservices on the Kubernetes platform. So, they can start by migrating their services once or twice and monitor them to make sure everything is running stable. Once they feel everything is going good, then they can migrate the rest of the application into their Kubernetes cluster.

Scenario 2: Consider a multinational company with a very much distributed system, with a large number of data centers, virtual machines, and many employees working on various tasks.

How do you think can such a company manage all the tasks in a consistent way with Kubernetes?

Solution:

As all of us know that I.T. departments launch thousands of containers, with tasks running across a numerous number of nodes across the world in a distributed system.

In such a situation the company can use something that offers them agility, scale-out capability, and DevOps practice to the cloud-based applications.

So, the company can, therefore, use Kubernetes to customize their scheduling architecture and support multiple container formats. This makes it possible for the affinity between container tasks that gives greater efficiency with an extensive support for various container networking solutions and container storage.

Scenario 3: Consider a situation, where a company wants to increase its efficiency and the speed of its technical operations by maintaining minimal costs.


How do you think the company will try to achieve this?

Solution:

The company can implement the DevOps methodology, by building a CI/CD pipeline, but one problem that may occur here is the configurations may take time to go up and running. So, after implementing the CI/CD pipeline the company’s next step should be to work in the cloud environment. Once they start working on the cloud environment, they can schedule containers on a cluster and can orchestrate with the help of Kubernetes. This kind of approach will help the company reduce their deployment time, and also get faster across various environments.

Scenario 4:  Suppose a company wants to revise it’s deployment methods and wants to build a platform which is much more scalable and responsive.

How do you think this company can achieve this to satisfy their customers?

Solution:

In order to give millions of clients the digital experience they would expect, the company needs a platform that is scalable, and responsive, so that they could quickly get data to the client website. Now, to do this the company should move from their private data centers (if they are using any) to any cloud environment such as AWS. Not only this, but they should also implement the microservice architecture so that they can start using Docker containers. Once they have the base framework ready, then they can start using the best orchestration platform available i.e. Kubernetes. This would enable the teams to be autonomous in building applications and delivering them very quickly.

Scenario 5: Consider a multinational company with a very much distributed system, looking forward to solving the monolithic code base problem.

How do you think the company can solve their problem?

Solution

Well, to solve the problem, they can shift their monolithic code base to a microservice design and then each and every microservices can be considered as a container. So, all these containers can be deployed and orchestrated with the help of Kubernetes.



Scenario 6: All of us know that the shift from monolithic to microservices solves the problem from the development side, but increases the problem at the deployment side.

How can the company solve the problem on the deployment side?

Solution

The team can experiment with container orchestration platforms, such as Kubernetes and run it in data centers. So, with this, the company can generate a templated application, deploy it within five minutes, and have actual instances containerized in the staging environment at that point. This kind of Kubernetes project will have dozens of microservices running in parallel to improve the production rate as even if a node goes down, then it can be rescheduled immediately without performance impact.

Scenario 7:  Suppose a company wants to optimize the distribution of its workloads, by adopting new technologies.

How can the company achieve this distribution of resources efficiently?

Solution

The solution to this problem is none other than Kubernetes. Kubernetes makes sure that the resources are optimized efficiently, and only those resources are used which are needed by that particular application. So, with the usage of the best container orchestration tool, the company can achieve the distribution of resources efficiently.

Scenario 8: Consider a carpooling company wants to increase their number of servers by simultaneously scaling their platform.

How do you think will the company deal with the servers and their installation?

Solution

The company can adopt the concept of containerization. Once they deploy all their application into containers, they can use Kubernetes for orchestration and use container monitoring tools like Prometheus to monitor the actions in containers. So, with such usage of containers, giving them better capacity planning in the data center because they will now have fewer constraints due to this abstraction between the services and the hardware they run on.

Scenario 9: Consider a scenario where a company wants to provide all the required hand-outs to its customers having various environments.

How do you think they can achieve this critical target in a dynamic manner?

Solution

The company can use Docker environments, to put together a cross-sectional team to build a web application using Kubernetes. This kind of framework will help the company achieve the goal of getting the required things into production within the shortest time frame. So, with such a machine running, the company can give the hands-outs to all the customers having various environments.

Scenario 10: Suppose a company wants to run various workloads on different cloud infrastructure from bare metal to a public cloud.

How will the company achieve this in the presence of different interfaces?

Solution

The company can decompose its infrastructure into microservices and then adopt Kubernetes. This will let the company run various workloads on different cloud infrastructures.



Multiple Choice Interview Questions

This section of questions will consist of multiple-choice interview questions, that are frequently asked in interviews.

Q1. What are minions in the Kubernetes cluster? 

    They are components of the master node.
    They are the work-horse / worker node of the cluster.[Ans]
    They are monitoring engine used widely in kubernetes.
    They are docker container service.

Q2. Kubernetes cluster data is stored in which of the following?



    Kube-apiserver
    Kubelet
    Etcd[Ans]
    None of the above

Q3. Which of them is a Kubernetes Controller?

    ReplicaSet
    Deployment
    Rolling Updates
    Both ReplicaSet and Deployment[Ans]

Q4. Which of the following are core Kubernetes objects?

    Pods
    Services
    Volumes
    All of the above[Ans]

Q5. The Kubernetes Network proxy runs on which node?

    Master Node
    Worker Node
    All the nodes[Ans]
    None of the above

Q6. What are the responsibilities of a node controller?

    To assign a CIDR block to the nodes
    To maintain the list of nodes
    To monitor the health of the nodes
    All of the above[Ans]

Q7. What are the responsibilities of Replication Controller?

    Update or delete multiple pods with a single command
    Helps to achieve the desired state
    Creates a new pod, if the existing pod crashes
    All of the above[Ans]

Q8. How to define a service without a selector?

    Specify the external name[Ans]
    Specify an endpoint with IP Address and port
    Just by specifying the IP address
    Specifying the label and api-version

Q9. What did the 1.8 version of Kubernetes introduce?

    Taints and Tolerations[Ans]
    Cluster level Logging
    Secrets
    Federated Clusters

Q10. The handler invoked by Kubelet to check if a container’s IP address is open or not is?

    HTTPGetAction
    ExecAction
    TCPSocketAction[Ans]
    None of the above




:end:
#

[Top](#top)
<a name="#php5years-Q-A-2"></a>
#PHP Interview Questions And Answers For 5 Year Experience


PHP Experience Interview Questions

    How can we know the number of days between two given dates using PHP?
    How can we repair a MySQL table?
    How can we get the properties of an image (size, type, width, height) using php image functions?
    How can we take a backup of a mysql table and how can we restore it?
    What is a persistent cookie and how it is different from the Temporary cookie?
    How To Get the Uploaded File Information in the Receiving Script?
    What is the difference between mysql_fetch_object and mysql_fetch_array?
    What are the different tables present in MySQL?
    How can we encrypt the username and password using PHP?
    How can we send mail using JavaScript?
    What is the difference between ereg_replace() and eregi_replace()?
    How do I find out the number of parameters passed into a function?
    What’s the special meaning of __sleep and __wakeup?
    What is the difference between the functions unlink() and unset()?
    What is the difference between characters \023 and \x23?
    What’s the output of the ucwords function in this example?
    What’s the difference between htmlentities() and htmlspecialchars()?
    What are the different functions in sorting an array?
    How can we know the count/number of elements of an array?
    What is the maximum length of a table name, a database name, or a field name in MySQL?


#


PHP Interview Questions And Answers For 5 Year Experience

1) How can we know the number of days between two given dates using PHP?

A) Simple arithmetic:

    $date1 = date(‘Y-m-d’);
    $date2 = ‘2006-07-01’;
    $days = (strtotime() – strtotime()) / (60 * 60 * 24);
    echo “Number of days since ‘2006-07-01’: $days”;

2) How can we repair a MySQL table?

A) We can use REPAIR command to repair a table. The REPAIR command will repair the table specified.

The syntex for repairing a mysql table is:
REPAIR TABLE tablename
REPAIR TABLE tablename QUICK
REPAIR TABLE tablename EXTENDED

If QUICK is given, MySQL will do a repair of only the index tree.
If EXTENDED is given, it will create index row by row.

3) How can we get the properties of an image (size, type, width, height) using php image functions?

A) To know the Image type use exif_imagetype () function
To know the Image size use getimagesize () function
To know the image width use imagesx () function
To know the image height use imagesy() function

4) How can we take a backup of a mysql table and how can we restore it?

A) Create a full backup of your database:

    shell> mysqldump tab=/path/to/some/diropt db_name

Or

    shell> mysqlhotcopy db_name /path/to/some/dir

The full backup file is just a set of SQL statements, so restoring it is very easy:

    shell> mysql “.”Executed”;
    mysql_close($link2);

5) What Is a Persistent Cookie and how it is different from Temporary cookie?

A) A persistent cookie is a cookie which is stored in a cookie file permanently on the browser’s computer. By default, cookies are created as temporary cookies which stored only in the browser’s memory. When the browser is closed, temporary cookies will be erased. You should decide when to use temporary cookies and when to use persistent cookies based on their differences:

    Temporary cookies cannot be used for tracking long-term information.
    Persistent cookies can be used for tracking long-term information.
    Temporary cookies are safer because no programs other than the browser can access them.
    Persistent cookies are less secure because users can open cookie files see the cookie values.

Read This Article: UI Developer Interview Questions

6) How To Get the Uploaded File Information in the Receiving Script?

A) Once the Web server received the uploaded file, it will call the PHP script specified in the form action attribute to process them. This receiving PHP script can get the uploaded file information through the predefined array called $_FILES. Uploaded file information is organized in $_FILES as a two-dimensional array as:

    $_FILES[$fieldName][‘name’] – The Original file name on the browser system.
    $_FILES[$fieldName][‘type’] – The file type determined by the browser.
    $_FILES[$fieldName][‘size’] – The Number of bytes of the file content.
    $_FILES[$fieldName][‘tmp_name’] – The temporary filename of the file in which

The uploaded file was stored on the server.

    $_FILES[$fieldName][‘error’] – The error code associated with this file upload.

The $fieldName is the name used in the <input name=”fieldName” type=”FILE,” />

7) What is the difference between mysql_fetch_object and mysql_fetch_array?

A) MySQL fetch object will collect first single matching record where mysql_fetch_array will collect all matching records from the table in an array

8) 14. What are the different tables present in MySQL?

A) Total 5 types of tables we can create

    MyISAM
    Heap
    Merge
    INNO DB
    ISAM

9) How can we encrypt the username and password using PHP?

A) You can encrypt a password with the following Mysql>SET PASSWORD=PASSWORD(“Password”);

Or

You can use the MySQL PASSWORD() function to encrypt username and password.

Example: INSERT into user (password, …) VALUES (PASSWORD($password”)), …);

10) How can we send mail using JavaScript?

A) No. There is no way to send emails directly using JavaScript.

But you can use JavaScript to execute a client side email program send the email using the “mailto” code.

Here is an example:

function myfunction(form)
{
tdata=document.myform.tbox1.value;
location=”mailto:mailid@domain.com?subject=…”;
return true;
}
PHP Developer Interview Questions And Answers For Experienced

11) What is the difference between ereg_replace() and eregi_replace()?

A) eregi_replace() function is identical to ereg_replace() except that it ignores case distinction when matching alphabetic characters.

12) How do I find out the number of parameters passed into function?

A) func_num_args() function returns the number of parameters passed in.

Also Read: AngularJS Interview Questions

13) What’s the special meaning of __sleep and __wakeup?

A) __sleep returns the array of all the variables than need to be saved, while __wakeup retrieves them.

14) What is the difference between the functions unlink() and unset()?

A) unlink() is a function for file system handling. It will simply delete the file in context.

unset() is a function for variable management. It will make a variable undefined.
Interview Questions For PHP Developer

15) What is the difference between characters \023 and \x23?

A) The first one is octal 23, the second is hex 23.

16) What’s the output of the ucwords function in this example?

$formatted = ucwords(“PHP interview questions for experienced”);
print $formatted;

A) ucwords() makes every first letter of every word capital.

What will be printed is PHP Interview Questions For Experienced.

17) What’s the difference between htmlentities() and htmlspecialchars()?

A) htmlspecialchars only takes care of <, >, single quote ‘, double quote ” and ampersand.

htmlentities translates all occurrences of character sequences that have different meaning in HTML.

18) What are the different functions in sorting an array?

A) Sorting functions in PHP:

    asort()
    arsort()
    ksort()
    krsort()
    uksort()
    sort()
    natsort()
    rsort()

19) How can we know the count/number of elements of an array?

A) In two ways, we can count the number of elements of an array:
a) sizeof($array) – This function is an alias of count()
b) count($urarray) – This function returns the number of elements in an array.

20) What is the maximum length of a table name, a database name, or a field name in MySQL?

A) The maximum length of a table name, database name and field name is:

Database name: 64 characters
Table name: 64 characters
Column name: 64 characters
PHP Mysql Interview Questions And Answers For 5 Years Experience

21) How many values can the SET function of MySQL take?

A) MySQL SET function can take zero or more values, but at the maximum it can take 64 values.

22) What are the other commands to know the structure of a table using MySQL commands except EXPLAIN command?

A) DESCRIBE table_name;

23) What’s the difference between md5(), crc32() and sha1() crypto on PHP?

A) The major difference is the length of the hash generated.

CRC32 is, evidently, 32 bits, while sha1() returns a 128 bit value, and md5() returns a 160 bit value.

This is important when avoiding collisions.

PHP Interview Questions And Answers For 5 Year Experience
24) How can we find the number of rows in a result set using PHP?

A) Here is how you can find the number of rows in a result set in PHP:

$result = mysql_query($any_valid_sql, $database_link);
$num_rows = mysql_num_rows($result);
echo “$num_rows rows found”;

25) How many ways we can we find the current date using MySQL?

A) We can find current date using MySQL in different ways, they are:

    SELECT CURDATE();
    SELECT CURRENT_DATE();
    SELECT CURTIME();
    SELECT CURRENT_TIME();

PHP Interview Quesetions And Answers For Senior Developers

26) How to read and display a HTML source from the website url?

A) $filename=”https://codingcompiler.com/”;
$fh=fopen(“$filename”, “r”);
while( !feof($fh) ){
$contents=htmlspecialchars(fgets($fh, 1024));
print “$contents”;
}
fclose($fh);
?>

PHP Interview Questions And Answers For 5 Year Experience
27) How we used $_get and $_post variable in PHP?

A) We know that when we use $_GET variable all data_values are display on our URL.So,using this we don’t have to send secret data (Like:password, account code). But using we can bookmarked the importpage.

We use $_POST variable when we want to send data_values without display on URL.And their is no limit to send particular amount of character.
Using this we can not bookmarked the page.

28) Why we use $_REQUEST variable?

A) We use $_REQUEST variable in PHP to collect the data_values from $_GET,$_POST and $_COOKIE variable.

29) How we use ceil() and floor() function in PHP?

A) ceil() is use to find nearest maximum values of passing value.

Ceil Example:
$var=6.5;
$ans_var=ceil($var);
echo $ans_var;

Output: 7

floor() is use to find nearest minimum values of passing value.

Floor Example:
$var=6.5
$ans_var=floor($var);
echo $ans_var;

Output: 6

30) What is the answer of following code echo 1< 2 and echo 1 >2 ?

A) Output of the given code are given below:
echo 1<2
output: 1

echo 1>2
output: no output
PHP Programming Interview Questions And Answers For Experienced

31) What is the difference b/w isset and empty?

A) The main difference b/w isset and empty are:

isset: This variable is used to handle functions and checked a variable is set even through it is empty.

empty: This variable is used to handle functions and checked either variable has a value or it is an empty string,zero0 or not set at all.

32) What do you understand about PHP accelerator ?

A) Basically PHP accelerator is used to boost up the performance of PHP programing language.We use PHP accelerator to reduce the server load and also use to enhance the performance of PHP code near about 2-10 times.In one word we can say that PHP accelertator is code optimization technique.

filetype:pdf
filetype:doc
filetype:txt

33) What is the functionality of MD5 function in PHP?

A) string md5(string)

It calculates the MD5 hash of a string. The hash is a 32-character hexadecimal number.

34) How can we know the number of days between two given dates using MySQL?

A) Use DATEDIFF()
SELECT DATEDIFF(NOW(),’2006-07-01′);

35) How can we change the data type of a column of a table?

A) ALTER TABLE table_name CHANGE colm_name same_colm_name [new data type]
PHP Experienced Interview Questions And Answers

36) How can we encrypt and decrypt a data presented in a table using MySQL?

A) You can use functions: AES_ENCRYPT() and AES_DECRYPT() like:
AES_ENCRYPT(str, key_str)
AES_DECRYPT(crypt_str, key_str)

37) How can I retrieve values from one database server and store them in other database server using PHP?

A) For this purpose, you can first read the data from one server into session variables. Then connect to other server and simply insert the data into the database.

PHP Interview Questions And Answers For 5 Year Experience
38) What are encryption functions in PHP?

A) CRYPT() and MD5()

39) How can we get second of the current time using date function?

A) $second = date(“s”);

40) How many ways we can give the output to a browser?

A) HTML output
PHP, ASP, JSP, Servlet Function
Script Language output Function
Different Type of embedded Package to output to a browser
PHP 5 Years Experience Interview Questions

41) How array_walk function works in PHP?

A) It is used to update the elements/index of an original array.
In array_walk, two parameter are required.
original array and an callback function, with use of we update the array.

42) How to get the 2nd highest salary of an employee, if two employees may have the same salary?

A) select salary from employee group by salary order by salary limit 1,1

43) How to find duplicate email records in users table?

A) SELECT u1.first_name, u1.last_name, u1.email FROM users as u1
INNER JOIN (
SELECT email FROM users GROUP BY email HAVING count(id) > 1
) u2 ON u1.email = u2.email;

44) How to set the header in CURL?

A) curl_setopt($ch, CURLOPT_HTTPHEADER, Array(“Content-Type: text/xml”));

45) How to redirect https to HTTP URL and vice versa in .htaccess?

A) Redirect https to http

RewriteEngine On
RewriteCond %{HTTPS} on
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]

Redirect http to https

RewriteEngine on
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]
PHP Logical Interview Questions And Answers

46) What is the use of explode() function ?

A) This function is used to split a string into an array. Syntax : array explode( string $delimiter , string $string [, int $limit ] );

47) What is the use of mysql_real_escape_string() function?

A) mysql_real_escape_string() function mainly used to escapes special characters in a string for use in an SQL statement

48) What are Traits?

A) Traits are a mechanism that allows you to create reusable code in PHP where multiple inheritance is not supported. To create a Traits we use keyword trait.

49) Can you write source code to demonstrate Traits?

A) Example of Traits

trait users {
function getUserType() { }
function getUserDescription() { }
function getUserDelete() { }
}

class ezcReflectionMethod extends ReflectionMethod {
use users;
}

class ezcReflectionFunction extends ReflectionFunction {
use users;
}

50) How to start displaying errors in PHP application?

A) Add following code in PHP.

ini_set(‘display_errors’, 1);
ini_set(‘display_startup_errors’, 1);
error_reporting(E_ALL);

OR Add following code in .htacess

php_flag display_startup_errors on
php_flag display_errors on
php_flag html_errors on
php_flag log_errors on
:end:







