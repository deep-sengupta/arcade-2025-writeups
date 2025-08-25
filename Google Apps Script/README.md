# Google Apps Script: Access Google Sheets, Maps & Gmail in 4 Lines of Code (GSP235)

https://github.com/user-attachments/assets/65748248-7239-41be-b775-e5021858f349

---

## Task 1: Create a New Google Sheet and Enter a Street Address
  - Open **Google Sheets**.
  - On the blank spreadsheet, click into the first cell (A1, top-left corner).
  - Enter a valid street address with city/state or postal code. Example:
    ```
    76 9th Ave, New York, NY
    ```

## Task 2: Open Apps Script
  - Open the Apps Script editor: **Extensions > Apps Script**
  - This provides a code editor for creating a Sheets-bound script.

## Task 3: Add Script Code
  - Replace the default `Code.gs` template code with the following:
    ```javascript
    function sendMap() {
        var sheet = SpreadsheetApp.getActiveSheet();
        var address = sheet.getRange("A1").getValue();
        var map = Maps.newStaticMap().addMarker(address);
        GmailApp.sendEmail("<YOUR_EMAIL>", "Map", 'See below.', {attachments:[map]});
    }
    ```
  - Important: Replace <YOUR_EMAIL> with the lab-provided user email.
  - Save your project.

## Task 4: Run the Google Sheets, Maps, and Gmail App
  - Select the function sendMap to run:
    - Click Run in the Apps Script menu.

  - Review permissions:
    - Choose your account.
    - Click Allow for the app to access your Google Account.

  - Monitor execution:
    - On the left panel, click Executions to view sendMap.

  - Check your email:
    - Open Gmail and log in with your student credentials.
    - Accept terms if prompted.
