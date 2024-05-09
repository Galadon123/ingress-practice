# INGRESS

<P>In Kubernetes, Ingress is an API object that manages external access to services within a cluster. It provides HTTP and HTTPS routing to services based on defined rules. Essentially, it acts as a way to expose HTTP and HTTPS routes from outside the cluster to services running inside the cluster.</P>

<image src="./images/ingress.png" width="600">

# HOW INGRESS WORKS

**1.Ingress Controller**: Kubernetes itself doesn't implement the actual features of the Ingress. Instead, it relies on an Ingress controller, which is a daemon that runs within the cluster. The Ingress controller is responsible for actually implementing the rules specified in the Ingress resources.

Popular Ingress controllers include LOAD-BALANCER(GCE),NGINX Ingress Controller, Traefik, and HAProxy Ingress.Out of these LOAD-BALANCER(GCE) and nginx ingress conttroller is is mostly used.

<image src="./images/1.png" width="600">

#### NGINX-INGRESS-CONTROLLER:

NGINX Ingress Controller: NGINX is a widely used web server and reverse proxy server. The NGINX Ingress Controller extends its functionality to manage external access to services in Kubernetes clusters. It's known for its robustness, performance, and flexibility in handling HTTP, HTTPS, and TCP traffic.

**2.Ingress Resource**: This is where you define how you want incoming traffic to be routed to your services. It specifies rules like hostnames, paths, and backend services to which requests should be forwarded.

**3.Backend Services**: These are the services running within your Kubernetes cluster that you want to expose to the outside world. The Ingress resource forwards incoming requests to these backend services based on the defined rules.

**4.Load Balancing and SSL Termination**: Ingress controllers often integrate with cloud providers' load balancers or provide their own load balancing mechanisms to distribute traffic among backend services. They can also handle SSL termination, decrypting incoming HTTPS traffic before forwarding it to backend services.

## Steps to run this project locally

**1.Clone the project in your local directory**:

In our desired directory open cmd and apply this command

``
git clone https://github.com/Galadon123/ingress-practice.git
``

**2.Run the Definition files**

definition file for server1 and server2:

``
kubectl apply -f deployment1.yaml
``

``
kubectl apply -f deployment2.yaml
``

> **Please wait momentarily as the image is being pulled from Docker Hub and the deployment is initiated, ensuring it is running seamlessly.**

Service definition file for server1 and server2

``
kubectl apply -f svc1.yaml
``

``
kubectl apply -f svc2.yaml
``

Definition file for nginx-ingress-controller and nginx-ingress service and nginx-configuration

``
kubectl apply -f nginx-deploy.yaml
``

``
kubectl apply -f svc.yaml
``

``
kubectl apply -f configmap.yaml
``

Definition file for sepcifing backend services

``
kubectl apply -f ingress-resources.yaml
``

**3.Accressing the Service from outside the cluster.**

### What is minikube tunnel?

<p>Minikube tunnel establishes a secure route between your local machine and the services running inside the Minikube cluster, enabling you to access those services as if they were running in a real production environment.For a detailed example see..</p>

[Minikube Tunnel Documentation](https://minikube.sigs.k8s.io/docs/tasks/loadbalancer)
 
To access our implementd ingress implentation run minikube tunnel in you machine by using this command

``
minikube tunnel
``

To access server1 and server2 from local browser use http://127.0.0.1/server1 , http://127.0.0.1/server2






