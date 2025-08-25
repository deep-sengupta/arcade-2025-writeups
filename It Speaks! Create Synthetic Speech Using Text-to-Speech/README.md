# It Speaks! – Create Synthetic Speech Using Text-to-Speech (GSP222)

https://github.com/user-attachments/assets/7390acd1-9da6-4aca-a2a0-e232a9cba62d

---

## Set the Region
- Configure the default region for the project:
  ```bash
  gcloud config set compute/region Region
  ```

## Task 1: Enable the Text-to-Speech API
- Navigate to **APIs & Services → Library**
- Search: `text-to-speech`
- Select: **Cloud Text-to-Speech API**
- Click: **Enable**

## Task 2: Create a Virtual Environment
- Install virtualenv:
  ```bash
  sudo apt-get install -y virtualenv
  ```
- Create environment:
  ```bash
  python3 -m venv venv
  ```

- Activate environment:
  ```bash
  source venv/bin/activate
  ```

## Task 3: Create a Service Account
- Create service account:
  ```bash
  gcloud iam service-accounts create tts-qwiklab
  ```

- Generate key:
  ```bash
  gcloud iam service-accounts keys create tts-qwiklab.json --iam-account tts-qwiklab@Project ID.iam.gserviceaccount.com
  ```

- Export credentials:
  ```bash
  export GOOGLE_APPLICATION_CREDENTIALS=tts-qwiklab.json
  ```
