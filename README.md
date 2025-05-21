# Deploy to LKE Cluster from Jenkins Pipeline

## **Project Overview**
This project demonstrates how deploy to LKE cluster from jenkins pipeline. 

---
  
## **Feature**
- Create Linode k8 cluster.
- Download the kubeconfig file to connect to the cluster using kubectl command.
- Using KUBECONFIG=~/eks/test-kubeconfig.yaml.
- To point to another cluster “export KUBECONFIG=~/eks/test-kubeconfig.yaml
- Add LKE credentials on jenkins so that jenkins can have access to linode cluster.
- From credentials select secret file type and upload the kubeconfig file.
- Install the K8 CLI plugin for jenkins.
- Kubectl inside jenkins container.
- Install Kubernetes CLI jenkins plugin.
- From manage plugins select Kubernetes CLI plugin install and restart jenkins server.
- Ssh back into the container to restart.
- Configure jenkins to deploy to LKE cluster. Using the plugin called with KubeConfig withKubeConfig([credentilsID: ID_NAME’, serverUrl: endpoint of server])
- Build the job.
