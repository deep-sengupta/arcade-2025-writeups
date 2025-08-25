# Deploy Kubernetes Load Balancer Service with Terraform (GSP233)

https://github.com/user-attachments/assets/1a16b83b-c9a6-4809-9596-534b041c9e50

---

## Task 1: Clone the Sample Code
- Clone sample code:
  ```bash
  gsutil -m cp -r gs://spls/gsp233/* .
  ```

- Navigate to directory:
  ```bash
  cd tf-gke-k8s-service-lb
  ```

## Task 2: Understand the Code
- View the main Terraform configuration:
  ```bash
  cat main.tf
  ```

- (Optional) View the Kubernetes configuration:
  ```bash
  cat k8s.tf
  ```

## Task 3: Initialize and Install Dependencies
- Initialize Terraform:
  ```bash
  terraform init
  ```

- Apply Terraform configuration:
  ```bash
  terraform apply -var="region=[REGION]" -var="location=[ZONE]"
  ```

- Confirm Terraform actions:
  ```bash
  yes
  ```
