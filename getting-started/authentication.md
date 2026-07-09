Authentication
The FlowSync API uses API key authentication. Every request must include a
valid API key in the request header. This guide explains how to generate,
use, and manage your API keys.
---
How Authentication Works
FlowSync authenticates requests using a Bearer token in the
`Authorization` header. Include your API key in every request as follows:
```bash
Authorization: Bearer YOUR_API_KEY
```
Requests without a valid API key return a `401 Unauthorized` error.
---
Generating an API Key
Log in to your FlowSync dashboard at app.flowsync.io.
Click Settings in the left navigation panel.
Click API Keys under the Developer section.
Click Generate New Key.
Enter a descriptive name for the key — for example, "Production Integration" or "CI Pipeline."
Select the permission scope for the key:
Read only — the key can retrieve data but cannot create or modify resources
Read and write — the key can create, update, and delete resources
Admin — the key has full access including workspace settings
Click Create.
Copy the API key displayed on screen.
> **Note:** FlowSync displays your API key only once at creation. If you lose
> your key, you must generate a new one — existing keys cannot be retrieved.
Result: Your new API key appears in the API Keys list with the status
Active and the scope you selected.
---
Using Your API Key
Include your API key in the `Authorization` header of every request:
```bash
curl -X GET https://api.flowsync.io/v2/workflows \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```
Storing Your API Key Securely
Store your API key as an environment variable rather than hardcoding it in
your application:
```bash
# Set the environment variable
export FLOWSYNC_API_KEY="your_api_key_here"

# Use it in requests
curl -X GET https://api.flowsync.io/v2/workflows \
  -H "Authorization: Bearer $FLOWSYNC_API_KEY"
```
---
Managing API Keys
Viewing Your Keys
Your API Keys page at Settings > API Keys displays all active keys with:
Key name
Permission scope
Creation date
Last used date
Revoking a Key
Go to Settings > API Keys in your FlowSync dashboard.
Find the key you want to revoke.
Click Revoke next to the key name.
Click Confirm in the confirmation dialog.
Result: The key is immediately deactivated. Any requests using this key
return a `401 Unauthorized` error.
> **Note:** Revoking a key is permanent and cannot be undone. Make sure you
> have updated all systems using this key before revoking it.
---
Authentication Errors
Error Code	Message	Cause	Solution
401	`Unauthorized`	Missing or invalid API key	Check that your API key is correct and included in the `Authorization` header
401	`API key revoked`	The API key has been revoked	Generate a new API key
403	`Insufficient permissions`	The API key scope does not allow this action	Use a key with the required permission scope
---
Related Topics
Quickstart Guide — Make your first authenticated request
Error Codes — Full list of API error codes
