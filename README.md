#microk8s
https://ubuntu.com/tutorials/install-a-local-kubernetes-with-microk8s#1-overview

## enable addon
microk8s enable dns dashboard storage

## list namespace
microk8s kubectl get all --all-namespaces

## obtain token
token=$(microk8s kubectl -n kube-system get secret | grep default-token | cut -d " " -f1)  
microk8s kubectl -n kube-system describe secret $token  

## deploy sample
microk8s kubectl create deployment microbot --image=dontrebootme/microbot:v1  
microk8s kubectl scale deployment microbot --replicas=2  
microk8s kubectl expose deployment microbot --type=NodePort --port=80 --name=microbot-service  

look for NodePod Port  
access through chrome http://localhost:NodePod Port  