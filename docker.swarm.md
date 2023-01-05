# Docker Swarm


<a name="top"></a>
Topics: 

[Installation to click here](#docker_swarm_installations)

[Installation to click here](#docker_swarm_installations)













# Docker Swarm (installation): 

        docker info | head -50                   //Docker info; check swarm active or inactive

        docker swarm init                        //In master node

        doker node ls




# Creating three virtual machines (vm)

 1. master node (vm), worker1(vm) & worker2(vm) 


master node:

getting a token from master......this tokern and copy paste in worker1 and other token in worker2


workder1:

        paster token1 from master here
        docker swarm join-token master

worker2:

        paster token2 from master here
        docker swarm join-token master


        paster token3 from master here
        docker swarm join-token manager



docker node ls 


worker2:
        docker swarm leave  //This node is out from cluster
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


