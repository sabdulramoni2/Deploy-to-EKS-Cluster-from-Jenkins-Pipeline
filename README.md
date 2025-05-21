# Deploy to LKE Cluster from Jenkins Pipeline

## **Project Overview**
This project demonstrates how deploy to LKE cluster from jenkins pipeline. 

---
  
## **Feature**
- Create Linode k8 cluster.

  ![image](https://github.com/user-attachments/assets/4505fb6d-0c06-46bc-9b19-ed3a46772fea)

- Download the kubeconfig file to connect to the cluster using kubectl command.
- Using KUBECONFIG=~/eks/test-kubeconfig.yaml.
- To point to another cluster “export KUBECONFIG=~/eks/test-kubeconfig.yaml

  ![image](https://github.com/user-attachments/assets/7ccd833e-382d-4610-bafc-6a5f5da57eeb)


  ![image](https://github.com/user-attachments/assets/aa93cac3-f3ad-421a-adae-9b60c8d0e4dd)

- Add LKE credentials on jenkins so that jenkins can have access to linode cluster.
- From credentials select secret file type and upload the kubeconfig file.
- Install the K8 CLI plugin for jenkins.
- Kubectl inside jenkins container.
- Install Kubernetes CLI jenkins plugin.
- From manage plugins select Kubernetes CLI plugin install and restart jenkins server.
- Ssh back into the container to restart.
- Configure jenkins to deploy to LKE cluster. Using the plugin called with KubeConfig withKubeConfig([credentilsID: ID_NAME’, serverUrl: endpoint of server])

  ![image](https://github.com/user-attachments/assets/6c2fbe72-129d-477c-832b-9c0cdef4b1a6)

- Build the job.

  ![image](https://github.com/user-attachments/assets/4e929fee-98b8-4763-9ccf-e9342d2693d6)

  ![image](https://github.com/user-attachments/assets/9cc8f7dd-6013-4d4d-93e1-6f5b8649da6e)

