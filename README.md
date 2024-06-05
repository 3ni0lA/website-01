# Deploying a Scalable Web Application with Kubernetes
This guide walks you through deploying a simple web application with the following functionalities:

Highly Available Web Server: A multi-container web server ensures your application remains accessible even if one container experiences issues.
Automatic Scaling: The deployment automatically scales up or down the number of web server pods based on demand.
Load Balancing: An external load balancer distributes traffic across multiple web server pods, promoting consistent performance.
Simple User Interface: The deployed application displays a basic welcome message.

## Technologies Used:
Kubernetes: Container orchestration platform for automating deployment and management of containerized applications.
Docker: Tool for creating and managing container images.
Terraform (Optional): Infrastructure as Code tool for provisioning infrastructure resources on cloud platforms. (Not included in the provided code snippets)
Ansible (Optional): Configuration management tool for automating server configuration tasks. (Not included in the provided code snippets)

## Step-by-Step Guide:
1. Building the Web Application Image (Dockerfile):

The provided Dockerfile defines a simple web server image based on nginx:alpine. It copies the HTML file (index.html) to the default web server document root and sets the working directory for the container.

2. Creating the Deployment (deployment.yaml):

The deployment.yaml file defines a Kubernetes deployment named web-app-deploy. This deployment:

Specifies the desired number of replicas (3 in this case) for the web server pods.
Defines a pod selector that identifies pods with labels name: web-app-pod and app: website.
Creates a pod template that defines the container configuration for each web server pod. The template includes:
Container name: webapp01
Container image: 3niola/webapp (replace with your image location)
Exposed port: 80 (maps to the container port 80)
3. Creating the Service (service.yaml):

The service.yaml file defines a Kubernetes service named web-app. This service:

Exposes the web application externally using a LoadBalancer service type.
Defines a service port (80) that maps to the target port (80) of the web server pods.
Selects pods with labels name: web-app-pod and app: website for traffic routing.
4. Deploying the Application (Optional):

Use the kubectl apply -f deployment.yaml -f service.yaml command to deploy the application to your Kubernetes cluster.

5. Accessing the Application:

Once deployed, the service automatically creates a LoadBalancer with an external IP address. Access your application by browsing to this IP address in your web browser.

Impact:

This approach offers several benefits:

Scalability: You can easily scale your application by adjusting the number of replicas in the deployment.
High Availability: The deployment automatically restarts failed containers and spins up new ones if needed, ensuring application uptime.
Load Balancing: Traffic is distributed across multiple web server pods, improving performance and handling increased load.
Automation: Deployment and configuration are automated, reducing manual intervention.
Additional Notes:

This example provides a basic implementation. Production deployments might involve additional considerations like health checks, resource quotas, and container registry management.
You can integrate tools like Terraform and Ansible to automate infrastructure provisioning and server configuration tasks before deploying the application to Kubernetes.
By following these steps and understanding the concepts involved, you can leverage Kubernetes to deploy and manage your web applications in a scalable and reliable manner.
