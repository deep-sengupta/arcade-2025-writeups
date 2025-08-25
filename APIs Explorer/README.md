# APIs Explorer: Qwik Start (GSP277)

https://github.com/user-attachments/assets/94c3c527-e622-48a9-8dbe-92f36baf7bb1

---

## Task 1: Create a Cloud Storage Bucket
- Go to **Cloud Console > Cloud Storage > Buckets**.
- Click **Create bucket**.
- Enter a **unique bucket name** (do not include sensitive info). Example:
  ```
  PROJECT_ID-bucket
  ```
- Configure access.
- Click **Choose how to control access to objects**.
- Uncheck **Enforce public access prevention on this bucket**.
- Select **Fine-grained Access control**.
- Click **Create**.

## Task 2: Upload an Image
- Use your own image **or** download the demo image as `demo-image.jpg`.
- Upload the image to your bucket:
- Click **Upload > Upload Files** and select the image.
- Make the image public for API access:
- Click the **three vertical dots** (object overflow menu) next to your image.
- Select **Edit access**.
- In the overlay, click **+ Add entry**.
- Add permission for **allUsers**:
  - **Entity:** Public  
  - **Name:** allUsers  
  - **Access:** Reader
- Click **Save**.
