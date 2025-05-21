# Deploy to EKS Cluster from Jenkins Pipeline

## **Project Overview**
This project demonstrates how deploy to EKS cluster from jenkins pipeline. 

---
  
## **Feature**

### **Install kubectl command tools inside jenkins container**

- ssh into the server where jenkins is running as a container.
- Run docker exce to enter the container as a root user.
- Install kubectl with a curl command from the official source.

### **Installed aws-iam-authenticator inside Jenkins Container**

- Download the authenticator with curl
- Execute permission on it using
  ```
      chmod +x ./aws-iam-authenticator
  ```
- Move to local bin
  ```
       /usr/local/bin mv./aws-iam-authenticator /usr/local/bin
  ```
- Exit the container.

### **Created    ./kube/config and copied inside the Jenkins Container**

- Create the kubeconfig file manually on the host server and copy into the container.
- Vim config; copy the content from AWS documentation. Add the cluster name, server endpoint, certificate-authority-data.
- The certificate-authority-data is automatically generated in the kubeconfig. Copy and paste it.
- Now exec into the container, move into the home directory
  ```
       using  cd ~
  ```
- Create a new directory mkdir .kube in the home directory inside the container and exit the container.
- Copy the file using
  ```
       “docker cp config containerID;/var/jenkins_home/.kube/"
  ```
- The kubeconfigfile contains all the necessary information for authentication.

### **Add AWS credentials on jenkins for AWS account authentication**

- Create AWS IAM user for jenkins with limited permission.
- From the jenkins UI of the multibranch pipeline.
- Selects credentials and select the secret text for both access key and secret access key (jenkins_access_key_id   and jenkins_aws_secret_access_key_id).
- Now these credentials are available for jenkins to use.

### **Adjust jenkinsfile to configure EKS cluster deployment**

- First set up the env variable for the credentials.
  ```
        AWS_ACCESS_KEY_ID = credential(‘jenkins_access_key_id’)
        AWS_SECRET_ACCESS_KEY_ID = credentials(‘jenkins_aws_secret_access_key_id’)
  ```
  
- Using the shell script to deploy the image to our cluster.
  ```
      Sh ‘kubectl create deployment nginx-deployment –image=nginx’
  ```
