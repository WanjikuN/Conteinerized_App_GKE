#  Deploying Containerized App in GKE
## Prerequisites
  1. Enable API - Artifact Registry API, Cloud Build API , Kubernetes Engine API
  2. App
  3. Dockerfile
 ---
 
 ## Steps
  * Get your Google cloud project ID
      ```
      gcloud config get-value project
      ```
  * Create a repo in Artifact registry
      ```
      gcloud artifacts repositories create hello-repo \
    --project=PROJECT_ID \
    --repository-format=docker \
    --location=us-central1 \
    --description="Docker repository"
    
      ```
  * Build and push your image using cloud build
      ```
      gcloud builds submit --tag us-central1-docker.pkg.dev/PROJECT_ID/hello-repo/helloworld-gke .
      ```
  * Create a Cluster
      ```
      gcloud container clusters create-auto helloworld-gke --region us-central1
      ```
  * Deploy to GKE
    > Two objects . Deployment and Service
    1. Deploy the resource to the cluster
        ```
        kubectl apply -f deployment.yaml
        kubectl get deployments
        kubectl get pods
        ```
    1. Create service
        ```
        kubectl apply -f service.yaml
        kubectl get services
        ```
        
  ## View Deployed app
  ```
   http://EXTERNAL_IP
  ```
  ---
  
