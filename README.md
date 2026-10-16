Deploying Google's Online Boutique (Shopping Cart) Microservices Application on Kubernetes. This project deploys Google's Online Boutique (Shopping Cart) microservices application to a Kubernetes cluster hosted on Linode.

Each microservice is deployed using a Kubernetes Deployment and exposed internally using a Kubernetes Service.

### Deployment Design

Each microservice has its own Deployment and Service YAML definition.
Application services use environment variables to define connections to dependent services.
Redis is deployed as a standalone service and does not require environment variables.
The frontend service is exposed externally using a loadBalancer service.
All microservices are configured for high availability with 2 replicas.
Resource requests and limits are configured for CPU and memory.
Liveness and readiness probes are configured for health monitoring.
Redis operates as an infrastructure service. Redis is: The server Not the client Does not connect to other services Application services must know the Redis endpoint and therefore require environment variables that specify the Redis service address.

The container specs includes "livenessProbe" to check the if the microservice is available every 5 minutes. The "readinessProbe" to check if the service port is avialable. Containers are configured with resource limits for CPU and memory. For high availability all containers have 2 replicas.

### Create K8s cluster on Linode cloud

set the environment variable path to Linode's kubeconfig file
Test connection to Linode’s K8S cluster Kubectl get node

Deploy the microservices using "helmfile sync" command which will create the microservices defined in helmfile.yaml

### Alternate option

Included "install.sh" and "uninstall.sh" files to create and delete the microservices using the "helm install" and "helm uninstall" commands.