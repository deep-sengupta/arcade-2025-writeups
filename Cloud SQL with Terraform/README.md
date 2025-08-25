# Cloud SQL with Terraform (GSP234)

https://github.com/user-attachments/assets/b66f75e9-9eaf-436a-99c6-323eb6b8bb1c

---

## Task 1: Download Necessary Files
- Create a working directory:
  ```bash
  mkdir sql-with-terraform
  cd sql-with-terraform
  gsutil cp -r gs://spls/gsp234/gsp234.zip .
  ```

- Unzip the contents:
  ```bash
  unzip gsp234.zip
  ```

## Task 2: Understand the Code
- View the Terraform configuration:
  ```bash
  cat main.tf
  ```

## Task 3: Run Terraform

- Initialize Terraform:
  ```bash
  terraform init
  ```

- Create execution plan:
  ```bash
  terraform plan -out=tfplan
  ```

- Apply the plan:
  ```bash
  terraform apply tfplan
  ```
