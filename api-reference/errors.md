Error Codes
When a request fails, the FlowSync API returns an error response with a
JSON body describing the problem. This page lists all error codes and
explains how to resolve each one.
---
Error Response Format
All error responses follow this structure:
```json
{
  "error": {
    "code": "error_code",
    "message": "A human-readable description of the error.",
    "field": "field_name"
  }
}
```
The `field` property is only present for validation errors that relate to
a specific request parameter.
---
Authentication Errors (401)
Code	Message	Cause	Resolution
`missing_api_key`	No API key provided	The `Authorization` header is missing	Add `Authorization: Bearer YOUR_API_KEY` to your request
`invalid_api_key`	API key is invalid	The API key is incorrect or malformed	Verify you copied the full API key correctly
`api_key_revoked`	API key has been revoked	The key was revoked in the dashboard	Generate a new API key in Settings > API Keys
---
Authorization Errors (403)
Code	Message	Cause	Resolution
`insufficient_permissions`	API key does not have permission to perform this action	The key scope does not allow this operation	Use a key with the required scope (Read and Write or Admin)
`workspace_suspended`	This workspace has been suspended	The workspace account is suspended	Contact FlowSync support
---
Validation Errors (400)
Code	Message	Cause	Resolution
`missing_required_field`	The field is required	A required parameter was not included	Add the missing parameter to your request body
`invalid_field_value`	The field value is invalid	The parameter value does not match the expected format	Check the API reference for the correct format
`field_too_long`	The field exceeds the maximum length	A string parameter exceeds the character limit	Shorten the value
`invalid_status`	Status must be active, inactive, or draft	An invalid status value was provided	Use `active`, `inactive`, or `draft`
---
Not Found Errors (404)
Code	Message	Cause	Resolution
`workflow_not_found`	Workflow not found	The `workflow_id` does not exist	Verify the workflow ID is correct
`trigger_not_found`	Trigger not found	The `trigger_id` does not exist	Verify the trigger ID is correct
---
Rate Limit Errors (429)
Code	Message	Cause	Resolution
`rate_limit_exceeded`	Too many requests	You have exceeded the rate limit for your plan	Wait for the time specified in the `Retry-After` header before making the next request
When you receive a `429` error, check the `Retry-After` response header:
```
Retry-After: 30
```
This value is in seconds. Wait this duration before retrying the request.
---
Server Errors (500)
Code	Message	Cause	Resolution
`internal_server_error`	An unexpected error occurred	A server-side error occurred	Retry the request. If the error persists, contact FlowSync support at support@flowsync.io
`service_unavailable`	The service is temporarily unavailable	Scheduled maintenance or an outage	Check the FlowSync status page at status.flowsync.io
---
Handling Errors in Your Code
The following example shows how to handle FlowSync API errors:
```python
import requests

def create_workflow(api_key, name):
    response = requests.post(
        "https://api.flowsync.io/v2/workflows",
        headers={
            "Authorization": f"Bearer {api_key}",
            "Content-Type": "application/json"
        },
        json={"name": name, "status": "active"}
    )

    if response.status_code == 201:
        return response.json()
    elif response.status_code == 401:
        raise Exception("Authentication failed. Check your API key.")
    elif response.status_code == 429:
        retry_after = response.headers.get("Retry-After", 60)
        raise Exception(f"Rate limit exceeded. Retry after {retry_after} seconds.")
    else:
        error = response.json().get("error", {})
        raise Exception(f"API error: {error.get('message', 'Unknown error')}")
```
---
Related Topics
Authentication — Fix authentication errors
API Overview — HTTP status codes and response format
