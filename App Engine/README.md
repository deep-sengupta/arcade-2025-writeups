# App Engine: Qwik Start - Java (GSP068)

https://github.com/user-attachments/assets/a1b39f59-406d-4c55-a754-6e5f5adde684

---

## Task 1: Download the Sample HTTP Server App
- Open a new **Cloud Shell** session by clicking the **Activate Cloud Shell** button in the top right of the Cloud Console.
- Run the following command to copy the sample files from Cloud Storage:
  ```bash
  gcloud storage cp -r gs://spls/gsp068/appengine-java21/appengine-java21/* .
  ```
- Navigate to the sample code directory:
  ```bash
  cd helloworld/http-server
  ```

## Task 2: Deploy and View Your App
- Deploy the HTTP Server app to App Engine:
  ```bash
  gcloud app deploy
  ```
- When prompted:
  - Enter the number associated with your preferred REGION.
  - Type y to continue.
- View your deployed app:
  ```bash
  gcloud app browse
  ```
- Click the link to open your app in a web browser.<br>
You should see a simple web page displaying:
  ```ngnix
  Hello World!
  ```
