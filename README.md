
# Kubernetes architecture

 (Kubernets cluser < Master / Api Server [Node,Node{POD"Conainer,Container"POD"Container"}]>)

# Setup git, repository, git action (superlinter)
# Kuberntest lab setup

    vagrant up
    vangrant ssh
    sudo apt-get update
# Install Docker and requirements
  
    sudo apt-get install -y docker.io apt-transport-https ca-certificates curl software-properties-common gnupg2 conntrack
    sudo systemctl enable docker.service

# Install Minikube

    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \  && chmod +x minikube
    sudo mkdir -p /usr/local/bin/ && sudo install minikube /usr/local/bin/

# Start Minikube

sudo minikube start --vm-driver=none
sudo minikube status

# Kube controll install

    curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl
    kubectl version --client

# Creating aliases

    alias kubectl='sudo kubectl'
    alias k='sudo kubectl'
    alias minikube='sudo minikube'
    alias | grep -i sudo
    alias | grep -i sudo >> ~/.bashrc
    tail 10 ~/.bashrc
    k version
    k version --client
    minikube status
    k cluster-info

# Create Deployment

    k create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10
# Expose it as a service

    k expose deployment hello-minikube --type=NodePort --port=8080
  
 # Test, watch minikube
 
    k get pods
    k get svc
    curl 10.104.34.252:8080
    minikube service hello-minikube --url
    curl http://10.0.2.15:31272
    k logs hello-minikube-xxxxxxx
    
# Delete 

    k delete svc hello-minikube
    k delete deployment hello-minikube
    k get pods
    k get svc

# Cheking Node

    k get node
    k get node -o wide
    k describe node
    k get node -o yaml
    k get ns
    k get pods -n kube-system

# Create again

    k create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10
    k get pods

# Labels
    k get pod --show-labels
    k delete deployment hello-minikube 
    

# Create Pode with yml

   cd /vagrant/configs
   k create -f mypod1.yml
   k get pods
   k get pod --show-labels
   # this is dont work
   k apply -f mypod2.yml
   k delete pods mypod
   k get pods
   k create -f mypod2.yml
   k get node --show-labels
   k get node -L env
   sudo kubectl
# Annotations

   k annotate pod mypod notes='this is my first pod for testing kubernetes'
   k describe pod mypo d
   k annotate pod mypod apptypes='webserver'
   k describe pod mypod

# Name spaces

    k create -f custom-namespace.yml
    k get ns
    k create -f mypod-custom-ns.yml
    k get pods -n custom-namespace
    k get pods --all-namespaces


