#Kubernetes User Guide

One of the great things about Kubernetes is that it has loads of great documentation, which you can find here:
http://kubernetes.io/

All of the commands have great documentation too and adding --help to any command should give you loads of useful knowledge.

However, this breif guide should help you know the basics quickly.

### Kubernetes/Docker translation guide
######A lot of the commands in Docker have equivillent commands in Kubernetes. Here is a breif translation guide.


docker run -dit jenkins   ==    kubectl run my_jenkins --image=jenkins
  
docker ps   =   kubectl get po

docker exec -ti {container_ID} bash    =   kubectl exec -ti {pod_name} bash

docker logs {container_ID)    =     kubectl logs {pod_name}

docker rm -f {container_ID)   =   kubectl delete deployment {deployment_name}

### Browser interfaces
(Note if you are using the cloud you will need to setup tunneling to be able to access these through a browser.
Here is a helpful guide https://anapnea.net/tut_putty_tunneling.php.)


kubernetes-dashboard
This is the main GUI for kubernetes. From here you can manage both nodes and pods, as well as basic error checking.

Weavescope
This is a great visual tool for seeing how pods and services are distributed accross nodes.

### Useful things you can do with Kubernetes

    1.Label nodes
  
      Labelling nodes is very useful, easily allowing you to configure specific groups of nodes differently.
  
    2. Scale applications.
    
      This is very useful, allowing you to scale an application (creating and deleting containers as needed). 
      This can even be set to do this automatically depending on some metrics.
      To do this run: kubectl scale rc NAME --replicas = COUNT
      This will scale the NAME service to have COUNT replicas.
    
    3. Rollong update
  
      If you would like to update an application running in multiple containers on multiple nodes, with Kubernetes it's possible.
      To do this run: kubectl rolling-update NAME [NEW_NAME] --image=IMAGE
      This will uptdate the NAME service containers with containers from IMAGE. This will destroy and create the containers intelligently, making sure the numbers of containers is one less or one more than the number of containers.


