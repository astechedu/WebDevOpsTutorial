# Docker Swarm


<a name="top"></a>
Topics: 

[Installation to click here](#docker_swarm_installations)

[Creating three virtual machines & more cmds to click here](#threen_swm_cmds)








<a name="docker_swarm_installations"></a>

# Docker Swarm (installation): 

  Docker info; check swarm active or inactive

        docker info | head -50   
        
        
   In master node
 
        docker swarm init                       

        doker node ls




<a name="threen_swm_cmds"></a>
# Creating three virtual machines (vm)

 1. master node (vm) 
 2. worker1(vm) 
 3. worker2(vm) 


master node:

getting a token from master nodee......copy this token and  paste it in worker1 and other token in worker2 and save these tokens for future


workder1:

        paster token1 from master here
        docker swarm join-token master

worker2:

        paster token2 from master here
        docker swarm join-token master

worker3:

        paster token3 from master here
        docker swarm join-token manager



        docker node ls 


worker2:

//This node is out from cluster

        docker swarm leave  
        docker node ls

        docker swarm | head -50




  Manager: 
        
        docker node ls
        docker node rm 
        doker info less


        docker node inspect worker1 | less
        docker node inspect worker2 | less
        docker node promote worker1 worker2
        docker node promote worker1 worker2

        docker node ls

        doker container run -it alpine ping 102.168.25.10












# How to Install and Configure Docker Swarm on Ubuntu

 Manager Nodes and Worker Nodes

Docker Swarm is made up of two main components:

    Manager Nodes
    Worker Nodes



 Getting Started:

Before starting, you should update your system repository with the latest version. You can update it with the following command:

        sudo apt-get update -y && sudo apt-get upgrade -y 

Once the repository is updated, restart the system to apply all the updates.



Install Docker:



You will also need to install the Docker engine on both nodes. By default, Docker is not available in the Ubuntu 16.04 repository. So you will need to set up a Docker repository first. You can start by installing the required packages with the following command:

sudo apt-get install apt-transport-https software-properties-common ca-certificates -y 

Next, add the GPG key for Docker: 

        wget https://download.docker.com/linux/ubuntu/gpg && sudo apt-key add gpg 

Then, add the Docker repository and update the package cache: 

sudo echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" >> /etc/apt/sources.list 

        sudo apt-get update -y 
        
Finally, install the Docker engine using the following command: 

        sudo apt-get install docker-ce -y 

Once the Docker is installed, start the Docker service and enable it to start on boot time: 

        sudo systemctl start docker && sudo systemctl enable docker By default, 



Configure firewall



You will need to configure firewall rules for a swarm cluster to work properly on both nodes. Allow the ports 7946, 4789, 2376, 2376, 2377, and 80 using the UFW firewall with the following command:


sudo ufw allow 2376/tcp && sudo ufw allow 7946/udp && sudo ufw allow 7946/tcp && sudo ufw allow 80/tcp && sudo ufw allow 2377/tcp && sudo ufw allow 4789/udp Next, reload the UFW firewall and enable it to start on boot: sudo ufw reload && sudo ufw enable Restart the Docker service to affect the Docker rules: sudo systemctl restart docker



 Create Docker Swarm cluster:

First, you will need to initialize the cluster with the IP address, so your node acts as a Manager node. On the Manager Node, run the following command for advertising IP address:

docker swarm init --advertise-addr 192.168.0.103 You should see the following output:

Swarm initialized: current node (iwjtf6u951g7rpx6ugkty3ksa) is now a manager.

To add a worker to this swarm, run the following command:
    docker swarm join --token SWMTKN-1-5p5f6p6tv1cmjzq9ntx3zmck9kpgt355qq0uaqoj2ple629dl4-5880qso8jio78djpx5mzbqcfu 192.168.0.103:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.






