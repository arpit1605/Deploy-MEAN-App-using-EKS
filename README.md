# ResumeBuilder MEAN Application

## Create a CI/CD pipeline using Jenkins and deploy a MEAN application using EKS

## Overview

ResumeBuilder is a full-stack application built using the MEAN stack (MongoDB, Express.js, Angular, and Node.js) targeted at simplifying the resume creation process. This project requires Node.js version 18.

## Run Project Locally

### Setup

1. Clone the repository to your local system.

2. Create a `.env` file in the project root to store environment variables necessary for the application:

   ```
   MONGO_URL="mongodb+srv://<username>:<password>@cluster/resume_builder"
   JWT_SECRET_KEY="MYREALLYSECRETKEY"
   OPENAI_KEY="OPENAI_API_KEY"
   GMAIL_USER="user@example.com"
   GMAIL_PASS="emailpassword"
   FRONT_END="http://localhost:4200"
   ```

### Backend Setup

3. Navigate to the `ResumeBuilderBackend` directory.

4. Install the necessary dependencies and build the project:

   ```bash
   npm install
   npm install -g typescript
   tsc --build
   ```

5. Start the backend server:

   ```bash
   npm run start
   ```

6. Test the backend by accessing `http://localhost:4292`. If properly set up, you should see:

   ```
   Cannot GET /
   ```


### Frontend Setup

7. Move to the `ResumeBuilderAngular` directory.

8. Install Angular CLI and other necessary frontend dependencies:

   ```bash
   npm install -g @angular/cli
   npm install --force
   ```

9. Start the Angular application:

   ```bash
   npm start
   ```

10. Test the frontend by accessing `http://localhost:4200`.


### Congratulations

Your local setup is complete! Next, we'll proceed with Docker deployment.


## Docker Deployment

### Backend Deployment

1. In the `ResumeBuilderBackend` folder, create a `Dockerfile` that specifies the Node.js version, installs dependencies, and sets up the distribution file for execution.

2. Build and test the Docker image locally:

   ```bash
   docker build -t resume-builder-backend .
   docker run -p 4292:4292 resume-builder-backend
   ```

3. Test `http://localhost:4292` again to confirm the setup.

4. Push the Docker image to Docker Hub and AWS ECR:

   ```bash
   # Create a repository on AWS ECR
   aws ecr create-repository --repository-name resume-builder-backend --region us-east-1

   # Login to AWS ECR
   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com

   # Tag and push the Docker image
   docker tag resume-builder-backend:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/resume-builder-backend:latest
   docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/resume-builder-backend:latest
   ```


### Frontend Deployment

Repeat similar steps as backend deployment, ensuring you use port 4200 for the frontend.

## Docker Compose

1. Create a `docker-compose.yaml` file to define and run multi-container Docker applications.

2. Specify services, networks, and volumes as needed to run both the backend and frontend components.



## Kubernetes Deployment

### Cluster Creation

1. Create Kubernetes deployment and service YAML files to manage the pods, services, and overall ecosystem.

2. Apply the Kubernetes configurations:

   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

3. Verify the deployment:

   ```bash
   kubectl get deployments
   kubectl get pods
   kubectl get svc
   ```


### Minikube

To view the deployment on Minikube:

```bash
minikube dashboard
minikube service resume-builder-backend-svc
```

Open the displayed URL in a browser to view the result.

