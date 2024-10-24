# Python Flask Kubernetes Deployment

This project demonstrates a simple Python Flask application deployed on Kubernetes using Minikube. The application returns a greeting message and is accessible via a NodePort service.

## Project Structure

- `app.py`: The Flask application code.
- `Dockerfile`: Instructions to build the Docker image for the Flask app.
- `requirements.txt`: Python dependencies for the Flask app.
- `deployment.yml`: Kubernetes deployment and service configuration.

## Prerequisites

- Docker Installed
- Minikube Installed
- kubectl configured to interact with your Minikube cluster

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

### Step 3: Build the Docker Image

Navigate to the project directory and build the Docker image:

```bash
docker build -t your-dockerhub-username/python-app:3.0 .
```
### Step 4: Log in to Docker Hub

Authenticate with Docker Hub, Enter username and password:

```bash
docker login
```

### Step 5: Push the Docker Image

Push the Docker image to Docker Hub:

```bash
docker push your-dockerhub-username/python-app:3.0
```

### Step 6: Deploy to Kubernetes

Apply the Kubernetes deployment and service configuration:

```bash
k apply -f deployment.yml
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
