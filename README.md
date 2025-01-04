# Python Flask Kubernetes Deployment

This project demonstrates deploying a simple Python Flask application on Kubernetes using Minikube and Helm. The application provides a greeting message and is accessible via a NodePort service.

## Project Structure

- `app.py`: The Flask application code.
- `Dockerfile`: Instructions to build the Docker image for the Flask app.
- `requirements.txt`: Python dependencies for the Flask app.
- `deployment.yml`: Kubernetes deployment and service configuration.

Helm Chart Structure 
- `Chart.yaml`: Helm chart metadata.
- `values.yaml`: Default values for the Helm chart.
- `templates/deployment.yaml`: Kubernetes deployment template.
- `templates/service.yaml`: Kubernetes service template.
- `templates/ingress.yaml`: Kubernetes ingress template.
- `templates/serviceaccount.yaml`: Kubernetes service account template.
![alt text](image-1.png)

## Prerequisites

- Kubernetes cluster
- Helm 3.x installed
- Docker (for building the image)
- kubectl configured to connect to your cluster

### Note
Remember to enter the correct values for your helm chart name, release name, docker image name, and docker image tag.

## Setup Instructions

### Step 1: Start Minikube

Start Minikube with a specific Kubernetes version:

```bash
minikube start --kubernetes-version v1.30.0
```

### Step 2: Set Alias for kubectl

Create an alias for kubectl for convenience:

```bash
alias kubectl="minikube kubectl --"
```
### Step 3: Create Helm Chart
```bash
helm create <HelmChart-Name>
```
### Step 4: Changes Structure
  - Chart.yml: Make changes to this file as need be
  - values.yml:
    ○ Scroll to the image section, under it; For repository, enter the docker image or cloud service provider image repo name. For tag, enter the value for it, according to your image version. For pullPolicy, enter the value for it: Always
    ○ Scroll to service section, under it: For type, enter the type of service you want. For port, enter 80 according to your service. For targetPort, enter according to your application and remember the target port has to be the same as the port of your application.
  - template/service.yml:
    ○ Remember to update targetPort section to reference the variable:value that was parsed in the values.yml file. e.g.: targetPort: {{ .Values.service.targetPort }}
### Step 5: Leave the helm chart directory: 
  Go into the project directory
  ```bash
  cd ..
  ```
### Step 6: Build the Docker Image

Navigate to the project directory and build the Docker image:

```bash
docker build -t <docker-image-name>:<docker-image-tag> .
```
### Step 4: Log in to Docker Hub

Authenticate with Docker Hub, Enter username and password:

```bash
docker login
```

### Step 5: Push the Docker Image

Push the Docker image to Docker Hub:

```bash
docker push <docker-image-name>:<docker-image-tag>
```

### Step 6: Install Helm Chart

Install Helm Chart:

```bash
helm install <Release-name>  <./HelmChart-Directory-Name>
```
### Check Helm Release
```bash
helm list
```
### Step 7: Access the Application
Check the status of the deployment, pods, and service:

- View pods:

  ```
  k get pods
  ```

- View deployment:

  ```
  k get deployments
  ```

- View service:

  ```
  k get services

#### Option 1: Using Minikube Tunnel

Run the following command to create a tunnel and access the service directly in your browser:

```bash
minikube service my-service
```

This command will open the default web browser to the service URL.

## Notes

- Ensure that the Docker image name in `deployment.yml` matches the image you pushed to Docker Hub.
- The application is exposed on port 5000 inside the container and mapped to port 80 in the Kubernetes service.

## License

This project is licensed under the MIT License.
