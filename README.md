## Distributed Systems - Mini-project

**Icesi University**    
**Subject:** Distributed Systems   
**Professor:** Daniel Barragán C.  
**Topic:** Kubernetes   
**Students:**  
Alejandro Bueno	- A00335472  
Rubén Ceballos 	- A00054636  
Nicolás Recalde	- A00065888    
Ana Valderrama 	- A00065868   
**Git URL:** https://github.com/abc1196/sd2018b-project/tree/abueno/sd2018b-project  
  
### Goals  
* Identify the components involved in a kubernetes cluster.  
* Deploy a kubernetes cluster.  
* Deploy applications in a kubernetes cluster using its properties of persistent volumes, load balancing and service discovery.  
* Diagnos and execute autonomously the necessary actions to achieve stable infrastructures.  
  
### Prerequisites  
* Kubernetes Cluster  
  
### Description  
For this project we are going to deploy a kubernetes cluster with 3 nodes, one master and two workers. For that, we are going to use Google Cloud Platform, that provides a lot of benefits like: load balancing, automatic scaling, node pools, etc. To achieve this is necessary to follow a series of steps, provided in a easy Google guide (https://google.qwiklabs.com/focuses/878?locale=en&parent=catalog&qlcampaign=77-18-gcpd-236&utm_source=gcp&utm_medium=documentation).  
To demostrate the correct functioning of the cluster we are going to deploy a pod executing a web service. The deployment will have 3 replicas and each pod will have a label. This application could be accessed through the browser.  
  
### Development  
The goals of this project were achieved using Google Cloud Platform. First step is to log in to **Google Cloud Console**, if you have an GCP account is preferred to use the one provided for ***qwiklabs*** to not generate charges.  
Once we are in, it is necessary to activate Google Cloud Shell to access to command-line. When the environment is provisioned and connected, we can start. This shell is a virtual machine that has all the tools we will need.  
The project on Google Cloud is already created, so we have to set the default compute zone, and then it is ready to create the cluster.  
```  
gcloud config set compute/zone us-central1-a  
```    
A cluster consists of at least one machine, which corresponds to the master, an multiple worker machines called nodes. To create the cluster we run the following command:  
```   
gcloud container clusters create sd2018b-project  
```   
Where sd2018b-project corresponds to the name of the cluster. It is really simple, after the cluster is created. The credentials to access to it are needed so, we get it with the following command:  
```  
gcloud container clusters get-credentials sd2018b-project  
```  
Now, we are going to deploy a web aapplication, that will be accesible through the browser. We run the application on the cluster using a sample image provided by Google and we defined a port that container will expose.  
```  
kubectl run hello-server --image=gcr.io/google-samples/hello-app:1.0 --port 8080    
```   
Once we deploy the app, we created a kubernetes service to handle the external traffic, ***load balancer***, this create 2 additional nodes to handle requests (3 in total).  
```  
kubectl expose deployment hello-server --type="LoadBalancer"    
```  
![][1]  
**Figure 1.** Kubernetes cluster deployed with web server application and load balancing running.  

### Demonstration  
Once the nodes are running in the cluster, we can access to the web browser, and check that the web application is ok.    
![][2]  
**Figure 2.** Web application running.  
Afterwards, we deleted a node to see if the application contined running, we executed the following command:  
![][3]  
**Figure 3.** Command executed to delete a node and message showed.   
We appreciate only two nodes on console, so we went check the web service and it continued working.  
![][4]  
**Figure 4.** Active nodes.    
![][5]   
**Figure 5.** Web service running with only two nodes.  
### References  
* https://google.qwiklabs.com/focuses/878?locale=en&parent=catalog&qlcampaign=77-18-gcpd-236&utm_source=gcp&utm_medium=documentation 
  
[1]: images/kubernetes_full.png  
[2]: images/kubernetes_web_ok.png  
[3]: images/kubernetes_node_deleted.png  
[4]: images/kubernetes_nodes.png  
[5]: images/kubernetes_node_deleted_web_ok.png  
