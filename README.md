# AI Task Extraction Workflow using n8n

This project is an AI-powered automation workflow built with n8n.

The workflow receives messy task or meeting-style text through a webhook, uses AI to extract structured task details, saves the result, and returns a clean JSON response.

## Workflow

Webhook → AI Task Extraction → JSON Formatting → Save Result → Webhook Response

## Extracted Fields

- Task
- Owner
- Deadline
- Priority

## Example Input

```json
{
  "text": "Sara needs to send the client update today. Ahmed should prepare slides by Friday."
}