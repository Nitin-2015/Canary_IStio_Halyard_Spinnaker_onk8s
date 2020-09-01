
#### Setup Kubernetes (K8s) Cluster on AWS

1. Create Linux EC2 instance
1. install AWSCLI
   ```sh 
    curl https://s3.amazonaws.com/aws-cli/awscli-bundle.zip -o awscli-bundle.zip
    apt install unzip python
    unzip awscli-bundle.zip
    #sudo apt-get install unzip - if you dont have unzip in your system
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
    ```
    verify cli by aws --version
      ````
    1. Install kubectl
   ```sh
   curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl
   ```
1. Create an IAM user/role  with Route53, EC2, IAM and S3 full access
1. Attach IAM role to ubuntu server

    #### Note: If you create IAM user with programmatic access then provide Access keys. 
    Configure your AWS CLI credentials
        ```sh 
     $ aws configure
      AWS Access Key ID [None]: 
      AWS Secret Access Key [None]: 
      Default region name [None]: 
      Default output format [None]
  ```
    Install eksctl:#
    To install or upgrade eksctl on Linux using curl
    ```sh
    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
    eksctl version
   To create your aws eks cluster with eksctl
1. Create kubernetes cluster  
   ```sh 
    eksctl create  cluster \
--name sample \
--version 1.16 \
--region us-west-2 \
--node-type t3.large \
--nodegroup-name standard-workers \
--nodes 2 \
--nodes-min 1 \
--nodes-max 4 \
--managed
    ```
list the nodes .
   ```sh 
     kubectl get nodes 
   ```
 1. To delete cluster
    ```sh
     kops delete cluster sample --yes
    ```
