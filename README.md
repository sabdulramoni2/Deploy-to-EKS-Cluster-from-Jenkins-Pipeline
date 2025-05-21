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



## **Diagrammatic Presentation


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

  ![image](https://github.com/user-attachments/assets/4d43281d-2873-46a7-9f41-972326305b02)


### **Created    ./kube/config and copied inside the Jenkins Container**

- Create the kubeconfig file manually on the host server and copy into the container.
- Vim config; copy the content from AWS documentation. Add the cluster name, server endpoint, certificate-authority-data.

  ![image](https://github.com/user-attachments/assets/62d241d7-0ed8-4625-8dfc-6b6178c01775)

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

   ![image](https://github.com/user-attachments/assets/902bb880-a480-4ef2-81b8-aa0ae6eb9f02)
  
- The kubeconfigfile contains all the necessary information for authentication.


  ![image](https://github.com/user-attachments/assets/77d4bffb-ca3e-4738-9a8b-a38327b007da)



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

  ![image](https://github.com/user-attachments/assets/00698adf-7e5d-467c-a861-d0e905d74edf)


  ![image](https://github.com/user-attachments/assets/c42a0e10-f5a8-43b0-905a-ba2ed9b9ab5a)


  ![image](https://github.com/user-attachments/assets/d99243b7-d83d-40b3-8cd5-7878e37dfab2)


  ![image](https://github.com/user-attachments/assets/ab616ce9-c560-4c24-9656-6b9d82164b9f)


  ![image](https://github.com/user-attachments/assets/b4f3701a-d728-4263-9197-1380e56b1d6f)

  ### **These commands are used in the Deploy to EKS from Jenkins**

  #### **Install kubectl on Jenkins server**
  ```
     curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl; chmod +x ./kubectl; mv ./kubectl /usr/local/bin/kubectl
  ```

  
  #### **Install aws-iam-authenticator on Jenkins server**

  ```
      curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.6.11/aws-iam-authenticator_0.6.11_linux_amd64
      chmod +x ./aws-iam-authenticator
      mv ./aws-iam-authenticator /usr/local/bin
  ```

  #### **Copy config file to Jenkins server**
  ```
      docker cp config "YOUR DOCKER CONTAINER ID":/var/jenkins_home/.kube/
```
  

      
  





  
