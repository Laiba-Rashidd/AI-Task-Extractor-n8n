# AI Task Extraction Workflow using n8n

## Project Overview

This project is an AI workflow automation built using **n8n**. The workflow receives messy task or meeting-style text through a **webhook**, extracts structured task details, converts the result into JSON, saves the output as a local JSON file, and returns the structured response back to the webhook caller.

The goal of this project is to demonstrate a complete automation flow where unstructured text is processed into clean, useful task data.

## Objective

In real meetings, task discussions are often written in an unstructured way. For example, people may mention task owners, deadlines, and urgency in the middle of a paragraph. Manually reading such text and creating a task list takes time.

This workflow automates that process by extracting:

* Task
* Owner
* Deadline
* Priority

The final output is returned in structured JSON format and also saved locally.

## Core Workflow

```text
Webhook → Task Extraction → JSON Formatting → Local JSON Storage → Webhook Response
```

## Implemented n8n Flow

The final n8n workflow contains the following nodes:

```text
Webhook
↓
Code-based Task Extraction
↓
Convert to JSON
↓
Read/Write Files from Disk
↓
Prepare Response
↓
Respond to Webhook
```

## Features

* Receives input through an n8n webhook.
* Accepts messy task text or meeting-style discussion text.
* Extracts task details from unstructured input.
* Identifies task owner, deadline, and priority.
* Converts the extracted result into structured JSON.
* Saves the result as a local JSON file.
* Returns the structured response to the webhook caller.
* Can be tested using Postman.
* Includes exported n8n workflow JSON.
* Includes sample input and output files.
* Includes basic GitHub Actions validation.

## Extracted Fields

| Field      | Description                                |
| ---------- | ------------------------------------------ |
| `task`     | The actual action item to be completed     |
| `owner`    | The person responsible for the task        |
| `deadline` | The due date or time mentioned in the text |
| `priority` | Task priority such as High, Medium, or Low |

## Example Input

```json
{
  "text": "Sara needs to send the client update today. It is urgent. Ahmed should prepare the demo slides by Friday."
}
```

## Example Output

```json
{
  "success": true,
  "tasks": [
    {
      "task": "send the client update",
      "owner": "Sara",
      "deadline": "Today",
      "priority": "High"
    },
    {
      "task": "prepare the demo slides",
      "owner": "Ahmed",
      "deadline": "Friday",
      "priority": "Medium"
    }
  ]
}
```

## Project Structure

```text
AI-Task-Extractor-n8n/
│
├── README.md
├── .env.example
├── .gitignore
├── requirements.txt
│
├── workflow/
│   └── task-extractor-workflow.json
│
├── data/
│   ├── sample_inputs/
│   │   └── test_inputs.json
│   ├── sample_outputs/
│   │   └── sample_output.json
│   └── local_storage/
│
├── screenshots/
│   ├── workflow-canvas.png
│   ├── postman-response.png
│   └── local-json-output.png
│
└── .github/
    └── workflows/
        └── ci.yml
```

## Tools and Technologies Used

* n8n
* Webhook
* Code node
* Convert to File node
* Read/Write Files from Disk node
* Postman
* JSON
* GitHub Actions

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Laiba-Rashidd/AI-Task-Extractor-n8n.git
cd AI-Task-Extractor-n8n
```

### 2. Run n8n Locally

This project was built and tested using local n8n.

```bash
npx n8n@1.107.4
```

After n8n starts, open:

```text
http://localhost:5678
```

### 3. Import the Workflow

In n8n:

```text
Workflows → Import from File → Select workflow/task-extractor-workflow.json
```

### 4. Execute the Workflow

Open the imported workflow and click:

```text
Execute Workflow
```

In n8n test mode, the webhook URL only works after clicking **Execute Workflow**.

## Webhook Testing

Use Postman to test the workflow.

### Request Method

```text
POST
```

### Test URL

```text
http://localhost:5678/webhook-test/task_extractor
```

### Body Type

```text
raw JSON
```

### Sample Request Body

```json
{
  "text": "Sara needs to send the client update today. It is urgent. Ahmed should prepare the demo slides by Friday."
}
```

## Local JSON Storage

The extracted output is saved locally at:

```text
data/local_storage/tasks-output.json
```

This file is generated when the workflow runs.

## Sample Test Inputs

Multiple test inputs are included in:

```text
data/sample_inputs/test_inputs.json
```

A sample output is included in:

```text
data/sample_outputs/sample_output.json
```

## Screenshots

The `screenshots/` folder contains proof of working functionality:

* n8n workflow canvas
* Postman request and response
* Local JSON output file

## GitHub Actions CI

A basic GitHub Actions workflow is included at:

```text
.github/workflows/ci.yml
```

The CI workflow validates:

* Required project files exist
* Exported n8n workflow JSON is valid
* Sample input JSON is valid
* Sample output JSON is valid

## Current Status

Completed:

* Webhook trigger created
* Task extraction logic added
* JSON response generated
* Local JSON storage implemented
* Workflow tested using Postman
* n8n workflow exported
* Sample inputs and outputs added
* Screenshots added
* Basic GitHub Actions validation added

## Limitations

* The current extraction logic is rule-based inside the n8n Code node.
* It works well for simple task sentences such as “Sara needs to...” or “Ahmed should...”.
* Complex meeting language may need a real AI model node for better understanding.
* Deadline parsing is currently limited to common words such as today, tomorrow, next week, and weekdays.

## Future Improvements

* Replace rule-based extraction with an actual AI model node.
* Add Google Sheets integration.
* Improve support for long and complex meeting transcripts.
* Add better date parsing for formats like “15 June” or “next Monday”.
* Add duplicate task detection.
* Add validation for missing owner, deadline, or priority.
* Add support for multiple storage options such as database or Google Sheets.

## Final Note

This project demonstrates a complete automation workflow using n8n. It receives messy text through a webhook, extracts structured task data, saves the result locally, and returns a clean JSON response to the caller.
