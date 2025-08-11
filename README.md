# DevOps Practice Project
This project demonstrates GitHub, Jenkins, Docker, and Kubernetes integration.

## Steps
1. Clone this repo to your local machine.
2. Build the Docker image:
   ```bash
   docker build -t devops-practice-app .
   ```
3. Run locally:
   ```bash
   docker run -p 3000:3000 devops-practice-app
   ```
4. Push to registry (Docker Hub or GitHub Container Registry).
5. Deploy to Kubernetes:
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```
6. Access the app using the service URL.
