# Speech to Text Transcription with the Cloud Speech API (GSP048)

https://github.com/user-attachments/assets/819dd7a8-2a5e-4c5b-bc72-7abaea1bd287

---

## Task 1: Create an API Key
- Go to **Navigation menu > APIs & services > Credentials**.
- Click **Create credentials** → select **API key**.
- Copy and save the generated key.
- Click **Close**.
- Connect to the `linux-instance` VM via SSH:
  - Go to **Navigation menu > Compute Engine > VM Instances**.
  - Locate the `linux-instance` VM.
  - Click **SSH** to open the shell.
- In the SSH shell, export the API key (replace with your actual key):
  ```bash
  export API_KEY=<YOUR_API_KEY>
  ```

## Task 2: Create Your API Request
- Create a file for the request:
  ```bash
  touch request.json
  ```
- Open `request.json` in an editor and add:
  ```bash
  {
    "config": {
        "encoding":"FLAC",
        "languageCode": "en-US"
    },
    "audio": {
        "uri":"gs://cloud-samples-data/speech/brooklyn_bridge.flac"
    }
  }
  ```
- Save the file.

## Task 3: Call the Speech-to-Text API
- Run the API request using curl:
  ```bash
  curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
  "https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json
  ```
- The response is saved in `result.json`.
- View the output:
  ```bash
  cat result.json
  ```

## Task 4: Speech-to-Text Transcription in Different Languages
- Edit `request.json` to change the language and audio file. Example (French):
  ```json
  {
    "config": {
        "encoding":"FLAC",
        "languageCode": "fr"
    },
    "audio": {
        "uri":"gs://cloud-samples-data/speech/corbeau_renard.flac"
    }
  }
  ```
- Run the curl command again.
- View the results:
  ```bash
  cat result.json
  ```
