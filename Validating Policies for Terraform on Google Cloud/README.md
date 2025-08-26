# Validating Policies for Terraform on Google Cloud (GSP1021)

https://github.com/user-attachments/assets/6fc46c1b-238f-4d70-bfe3-3c9ce5853f6d

---

## Task 1: Validate a Constraint

### Copy the Constraint
- Open a new **Cloud Shell** window and clone the policy library repository:
  ```bash
  git clone https://github.com/GoogleCloudPlatform/policy-library.git
  ```
- Navigate to the repo:
  ```bash
  cd policy-library/
  ```
- Copy the sample IAM domain restriction constraint:
  ```bash
  cp samples/iam_service_accounts_only.yaml policies/constraints
  ```
- Examine the copied constraint:
  ```bash
  cat policies/constraints/iam_service_accounts_only.yaml
  ```
- Test the Constraint
  - Create a Terraform file:
    ```bash
    touch main.tf
    ```
  - Open Cloud Shell Editor and edit `policy-library/main.tf` with the following:
    ```bash
    terraform {
      required_providers {
        google = {
          source = "hashicorp/google"
          version = "~> 3.84"
        }
      }
    }
    
    resource "google_project_iam_binding" "sample_iam_binding" {
      project = "<YOUR PROJECT ID>"
      role    = "roles/viewer"
    
      members = [
        "user:<USER>"
      ]
    }
    ```
  - Replace `<YOUR PROJECT ID>` with your Project ID.
  - Replace `<USER>` with your Lab username.

- Run Terraform Commands
  - Initialize Terraform:
    ```bash
    terraform init
    ```
  - Export the Terraform plan:
    ```bash
    terraform plan -out=test.tfplan
    ```
  - Convert the plan to JSON:
    ```bash
    terraform show -json ./test.tfplan > ./tfplan.json
    ```
  - Install Terraform Tools:
    ```bash
    sudo apt-get install google-cloud-sdk-terraform-tools
    ```
  - Validate the Terraform plan against your policies:
    ```bash
    gcloud beta terraform vet tfplan.json --policy-library=.
    ```

## Task 2: Modify the Constraint
- Open the file:
  ```
  policy-library/policies/constraints/iam_service_accounts_only.yaml
  ```
- Append the `qwiklabs.net` domain under `domains`:
  ```yaml
  apiVersion: constraints.gatekeeper.sh/v1alpha1
  kind: GCPIAMAllowedPolicyMemberDomainsConstraintV1
  metadata:
    name: service_accounts_only
  spec:
    severity: high
    match:
      target: ["organizations/**"]
    parameters:
      domains:
        - gserviceaccount.com
        - qwiklabs.net
  ```

- Revalidate the Plan
  - Export a new plan:
    ```bash
    terraform plan -out=test.tfplan
    ```
  - Validate again:
    ```bash
    gcloud beta terraform vet tfplan.json --policy-library=.
    ```

- Expected Output:
  ```nginx
  Validating resources...done.
  ```
- Apply the Terraform Plan
  - Apply the IAM policy:
    ```bash
    terraform apply test.tfplan
    ```
