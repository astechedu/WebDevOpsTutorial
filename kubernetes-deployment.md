# Kubernetes Deployment And More Basics


[Home]()

Topics: 

   [Create Pod](#create_pod)

   [Create Deployment](#create_deployment)










#

<a name="create_pod"></a>
# Create Pod

    Pod with HostPath: 

    apiVersion: v1
    kind: Pod
    metadata:
      name: hostpath2
      labels:
        app: php-vol1    
    spec:
      containers:
      - name: hostpath2
        image: astechutube/custom-php8.0-apache
        #command: ["/bin/bash", "-c", "sleep 15000"]
        volumeMounts:
         - name: testvol2
           mountPath: /var/www/html               
      volumes:
      - name: testvol2
        hostPath: 
          path: /tmp/php1 




#

<a name="create_deployment"></a>
# Create Deployment

    Deployment with hostpath

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: deploy-hostpath
      labels:
        app: host-vol1
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: host-vol1
      template:
        metadata:
          labels:
            app: host-vol1
        spec:
          containers:
          - name: hostpath
            image: astechutube/custom-php8.0-apache
            volumeMounts:
              - name: testvolume
                mountPath: /var/www/html         
            ports:
              - containerPort: 80
          volumes:
            - name: testvolume
              hostPath: 
                path: /tmp/var/www/html



CMDS: 

     microk8s kubectl apply -f deployment3.yml
     microk8s kubectl get deployment 
