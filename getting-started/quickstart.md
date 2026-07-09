Quickstart Guide
Get up and running with the FlowSync API in under 5 minutes. By the end of
this guide, you will have authenticated your first request and created a
simple workflow.
---
Prerequisites
Before you begin, make sure you have:
A FlowSync account (sign up at flowsync.io/signup)
A workspace created in your FlowSync dashboard
A terminal or API client such as Postman or curl
---
Step 1: Generate Your API Key
Log in to your FlowSync dashboard at app.flowsync.io.
Click Settings in the left navigation panel.
Click API Keys under the Developer section.
Click Generate New Key.
Enter a name for the key — for example, "My First Integration" — and click Create.
Copy the API key displayed on screen.
> **Note:** FlowSync displays your API key only once. Store it securely in a
> password manager or environment variable before closing this screen.
Result: Your API key is now active and ready to use. It appears in your
API Keys list with a status of Active.
---
Step 2: Make Your First Authenticated Request
Use the following request to verify your API key is working:
```bash
curl -X GET https://api.flowsync.io/v2/workspace \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```
Replace `YOUR_API_KEY` with the key you generated in Step 1.
Expected response:
```json
{
  "workspace_id": "ws_01abc123",
  "name": "My Workspace",
  "plan": "enterprise",
  "created_at": "2026-01-15T09:00:00Z"
}
```
Result: A `200 OK` response confirms your API key is valid and your
workspace is accessible.
---
Step 3: Create Your First Workflow
Send the following request to create a simple workflow:
```bash
curl -X POST https://api.flowsync.io/v2/workflows \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "My First Workflow",
    "description": "A simple test workflow",
    "status": "active"
  }'
```
Expected response:
```json
{
  "workflow_id": "wf_02xyz456",
  "name": "My First Workflow",
  "description": "A simple test workflow",
  "status": "active",
  "created_at": "2026-07-01T10:30:00Z"
}
```
Result: Your workflow is created and active. Note the `workflow_id` — you
will use it to add triggers and steps.
---
What's Next?
Now that your first workflow is running, you can:
Add a trigger to start the workflow automatically
Explore the Workflows API for advanced configuration
Review best practices for building reliable workflows
