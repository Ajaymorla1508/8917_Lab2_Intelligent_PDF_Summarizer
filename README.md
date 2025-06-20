# Lab 2: Intelligent PDF Summarizer (Azure Durable Functions)

## Overview

This project implements an **Intelligent PDF Summarizer** using Azure Durable Functions. The workflow is designed to process PDF files uploaded to Azure Blob Storage, extract their content, and generate a summary. Due to Azure OpenAI and Form Recognizer quota/permission limitations for student accounts, the AI and OCR steps are mocked to allow you to complete and submit the lab.

---

## Workflow

1. **Blob Trigger:**  
   Watches for new PDF files in the input container.

2. **Orchestrator Function:**  
   Coordinates the workflow:  
   - Calls `analyze_pdf` to extract text (mocked).
   - Calls `summarize_text` to generate a summary (mocked).
   - Writes the summary to the output container.

3. **Activity Functions:**  
   - `analyze_pdf`: Mocks PDF text extraction.
   - `summarize_text`: Mocks AI summarization.

---

## Mocking AI & OCR

Due to quota and permission issues, both the AI summarization and Form Recognizer steps are replaced with mock functions that return sample data.  
This allows the workflow to run end-to-end for lab submission.

---

## Project Structure

```
.
├── function_app.py         # Main Azure Functions app with orchestrator and activities
├── host.json              # Azure Functions host configuration
├── local.settings.json     # Local development settings (connection strings, etc.)
├── .vscode/
├── README.md              # This file
```

---

## Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd Intelligent-PDF-Summarizer
   ```

2. **Create and Activate Virtual Environment**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Local Settings**
   - Ensure your `local.settings.json` contains valid storage connection strings.
   - No Azure OpenAI or Form Recognizer keys are needed due to mocking.

5. **Run the Function App Locally**
   ```bash
   func start --verbose
   ```

6. **Test the Workflow**
   - Upload a PDF file to the configured input blob container.
   - The workflow will process the file and write a mock summary to the output container.

---

## Mock Function Details

### `analyze_pdf`
```python
@my_app.activity_trigger(input_name="context")
def analyze_pdf(context):
    # MOCK: Replace actual Form Recognizer call with a static result for lab completion
    return {
        "content": "This is mock extracted text from the PDF. Replace with your own sample if needed."
    }
```

### `summarize_text`
```python
@my_app.activity_trigger(input_name="context")
def summarize_text(context):
    # MOCK: Replace actual OpenAI call with a static summary for lab completion
    return "This is a mock summary of the PDF content. Replace this with your own summary text if desired."
```

---

## Common Issues & Solutions

- **Quota or Permission Errors:**  
  These are expected for student accounts. Mocking the AI and OCR steps resolves this.
- **Blob Storage Connection Errors:**  
  Ensure your `local.settings.json` uses the correct key:  
  `"BLOB_STORAGE_CONNECTION_STRING"` (not `"BLOB_STORAGE_ENDPOINT"`).

---

