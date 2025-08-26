# Extract, Analyze, and Translate Text from Images with the Cloud ML APIs (GSP075)

https://github.com/user-attachments/assets/05f7aa01-fcfe-4c66-955f-63522a4b8aed

---

## Task 1: Create an API Key
- Go to **Navigation menu > APIs & services > Credentials**.
- Click **+ Create Credentials** → select **API key**.
- Copy and save the generated key.
- Click **Close**.
- Save the API key to an environment variable (replace with your key):
  ```bash
  export API_KEY=<YOUR_API_KEY>
  ```

## Task 2: Upload an Image to a Cloud Storage Bucket

### Create a Cloud Storage Bucket
- Navigate to **Navigation menu > Cloud Storage browser** → click **Create bucket**.
- Enter a unique name:
  ```
  <PROJECT_ID>-bucket
  ```
- Click **Choose how to control access to objects**.
- Uncheck **Enforce public access prevention on this bucket**.
- Select **Fine-grained** access control.
- Click **Create**.

### Upload an Image
- Save the French sign image as `sign.jpg` to your computer.
- Navigate to your bucket in the **Cloud Storage browser**.
- Click **Upload > Upload files** → select `sign.jpg`.
- Make the file public:
- Click the **3 dots** next to the file → **Edit access**.
- Add entry:
  - **Entity:** Public  
  - **Name:** allUsers  
  - **Access:** Reader  
- Click **Save**.

## Task 3: Create Your Cloud Vision API Request
- In Cloud Shell, create `ocr-request.json`:
  ```bash
  nano ocr-request.json
  ```
- Add the following (replace `my-bucket-name` with your bucket name):
  ```bash
  {
    "requests": [
        {
          "image": {
            "source": {
                "gcsImageUri": "gs://my-bucket-name/sign.jpg"
            }
          },
          "features": [
            {
              "type": "TEXT_DETECTION",
              "maxResults": 10
            }
          ]
        }
    ]
  }
  ```

## Task 4: Call the Text Detection Method
- Call the Vision API:
  ```bash
  curl -s -X POST -H "Content-Type: application/json" --data-binary @ocr-request.json \
  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}
  ```
- Save the response:
  ```bash
  curl -s -X POST -H "Content-Type: application/json" --data-binary @ocr-request.json \
  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o ocr-response.json
  ```

## Task 5: Send Text from the Image to the Translation API
- Create `translation-request.json`:
  ```json
  {
    "q": "your_text_here",
    "target": "en"
  }
  ```
- Extract text from the OCR response and update the file:
  ```bash
  STR=$(jq .responses[0].textAnnotations[0].description ocr-response.json) && STR="${STR//\"}" && sed -i "s|your_text_here|$STR|g" translation-request.json
  ```
- Call the Translation API and save results:
  ```bash
  curl -s -X POST -H "Content-Type: application/json" --data-binary @translation-request.json \
  https://translation.googleapis.com/language/translate/v2?key=${API_KEY} -o translation-response.json
  ```
- View the response:
  ```bash
  cat translation-response.json
  ```

## Task 6: Analyzing the Image's Text with the Natural Language API
- Create `nl-request.json`:
  ```json
  {
    "document": {
      "type": "PLAIN_TEXT",
      "content": "your_text_here"
    },
    "encodingType": "UTF8"
  }
  ```
- Extract translated text into the file:
  ```bash
  STR=$(jq .data.translations[0].translatedText translation-response.json) && STR="${STR//\"}" && sed -i "s|your_text_here|$STR|g" nl-request.json
  ```
- Call the Natural Language API:
  ```bash
  curl "https://language.googleapis.com/v1/documents:analyzeEntities?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @nl-request.json
  ```
