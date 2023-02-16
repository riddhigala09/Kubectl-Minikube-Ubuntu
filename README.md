# Kubernetes-Minikube-Ubuntu
Demo to Install Kubernetes and Minikube On Ubuntu 21.10

In this demo, I will be installing Kubernetes and Minikube on Ubuntu 21.10.

Kubernetes will be installed on Docker version 20.10.17

Steps to Insatll Kubernetes(Kubectl):

1. Use terminal as root and change directory to root

   ![Screenshot from 2023-02-16 12-16-04](https://user-images.githubusercontent.com/122020679/219289160-fea2904d-8dd6-482c-abfc-d8f813c49776.png)
   
2. I'll be installing kubectl binary with curl on Linux.

   Dowload the latest version of kubectl using following command:
   
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   
   ![Screenshot from 2023-02-16 12-20-24](https://user-images.githubusercontent.com/122020679/219289796-a66b0d02-43c1-471b-af5f-9598c0dcdf39.png)

3. Download the Kubectl checksum file and validate it.

   Note: Download the same version of the binary and checksum, to avoid failure

   Download Command: curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
   
   ![Screenshot from 2023-02-16 12-21-43](https://user-images.githubusercontent.com/122020679/219290196-38a607c5-e4af-45c5-a17f-21e34bb8a7d6.png)
   
   Valdate cCommand: echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
   
   ![Screenshot from 2023-02-16 12-24-25](https://user-images.githubusercontent.com/122020679/219290583-6dc08606-e95f-4e03-81f9-a22f298dfaa1.png)
   
   Output:- kubectl: OK
   
4. Install Kuectl
   
   Command: sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
   
   ![Screenshot from 2023-02-16 12-27-40](https://user-images.githubusercontent.com/122020679/219291210-fcdd6770-3dfe-41ea-aef4-6228d6ff07bf.png)
   
   Kubectl will be installed in: /usr/local/bin/kubectl
   
   If you are not root user, you can still install kubectl to the ~/.local/bin directory:
   
   Enter following Commands:
   
   chmod +x kubectl                       #allows you to update file permission to executable
   
   mkdir -p ~/.local/bin                  #creates multiple directories
   
   mv ./kubectl ~/.local/bin/kubectl      #moves kubectl from directory it was installed to ~/.local/bin/kubectl
   
5. Check version of Kubectl

   Command: kubectl version --client
   
   ![Screenshot from 2023-02-16 12-37-06](https://user-images.githubusercontent.com/122020679/219292960-3d3fb357-5b76-437b-9487-ffc1743472c8.png)
   
   
6. Check that kubectl is configured properly by getting cluster state

   Command: kubectl cluster-info
   
   ![Screenshot from 2023-02-16 12-40-44](https://user-images.githubusercontent.com/122020679/219293661-eb295b7c-f77e-4609-b1e4-bf7b4a9e869e.png)

   I got this error because I am using Kubernetes Cluster(Kubectl) locally on my laptop. I will need to install Minikube and then re-run the above      command.
   
Steps to Install Minikube:

Platform Configs:

 > OS: Linux

 > Architecture: x86-64

 > Release type: Stable

 > Installer Type: Binary Download
 
If your platform is different then you can find more info on: https://minikube.sigs.k8s.io/docs/start/

1. Download Minikube with Curl:

   Command: curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   
   ![Screenshot from 2023-02-16 12-50-41](https://user-images.githubusercontent.com/122020679/219295427-c4571929-5721-4edc-b2f7-24a9d9bdf490.png)

2. Install Minikube

   Install Minikube in same directory as Kubectl, that is, /usr/local/bin

   Command: sudo install minikube-linux-amd64 /usr/local/bin/minikube
   
   ![Screenshot from 2023-02-16 12-52-15](https://user-images.githubusercontent.com/122020679/219295896-7976298f-af9a-45b2-a3e3-25c1f93c066d.png)
   
3. Check version of Minikube

   Command: minikube version
   
   ![Screenshot from 2023-02-16 12-56-03](https://user-images.githubusercontent.com/122020679/219296620-ac04b9d2-ce71-4d0b-95a3-81636f54021a.png)

4. Start cluster

   Exit from root and run following command.

   Command: minikube start
   
   This might take time.
   
   ![Screenshot from 2023-02-16 13-33-42](https://user-images.githubusercontent.com/122020679/219304417-a46c4818-b658-414e-bab4-00f3a5b29d64.png)

   Minikube started
   
   ![Screenshot from 2023-02-16 13-35-28](https://user-images.githubusercontent.com/122020679/219304729-3eda4135-2330-4558-8f22-4a19dec9a65e.png)

5. Checking cluster configuration

   re-reun the command: kubectl cluster-info
   
   ![Screenshot from 2023-02-16 13-37-17](https://user-images.githubusercontent.com/122020679/219305130-ec07d7b4-141d-4e14-be09-e682b819df7a.png)

6. Interact with cluster

   Command: kubectl get pods -A
  
   ![Screenshot from 2023-02-16 13-43-12](https://user-images.githubusercontent.com/122020679/219306331-d95d9e47-d4c6-40c2-a50f-fb45ce7973ec.png)

7. Access minikube dashboard

   Command: minikube dashboard
  
   ![Screenshot from 2023-02-16 13-46-26](https://user-images.githubusercontent.com/122020679/219306997-b3ede4d2-7cb7-49eb-a158-47dce54c6168.png)
 
   You will be redirected to Dashboard
  
   ![Screenshot from 2023-02-16 13-46-20](https://user-images.githubusercontent.com/122020679/219307171-161dead1-0066-4759-b9d7-9c1c2cfc3947.png)
  
8. To stop cluster

   Command: minikube stop
   
   ![Screenshot from 2023-02-16 13-49-23](https://user-images.githubusercontent.com/122020679/219308733-bf308b65-33ff-40f9-8c6d-273a34118305.png)

9. To delete cluster
 
   Command: minikube delete
   
   ![Screenshot from 2023-02-16 13-50-33](https://user-images.githubusercontent.com/122020679/219307919-6bdbecbc-74d5-4e5e-93e8-67ffe79d4989.png)


MINIKUBE HANDBOOK: https://minikube.sigs.k8s.io/docs/handbook/


   
   


   
