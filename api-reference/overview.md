API Overview
The FlowSync API is a RESTful API that allows you to create and manage workflows,
configure triggers, and retrieve execution data programmatically. This page
covers the API base URL, versioning, request format, and response structure.
---
Base URL
All API requests use the following base URL:
```
https://api.flowsync.io/v2
```
The current API version is v2. FlowSync maintains backward compatibility
within a major version. Breaking changes are released in a new major version
with at least 90 days advance notice.
---
Request Format
All requests must include the following headers:
Header	Value	Required
`Authorization`	`Bearer YOUR_API_KEY`	Yes
`Content-Type`	`application/json`	Yes for POST and PUT requests
Example Request
```bash
curl -X POST https://api.flowsync.io/v2/workflows \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Daily Report Workflow",
    "status": "active"
  }'
```
---
Response Format
All responses return JSON with the following structure:
Success Response
```json
{
  "workflow_id": "wf_02xyz456",
  "name": "Daily Report Workflow",
  "status": "active",
  "created_at": "2026-07-01T10:30:00Z"
}
```
Error Response
```json
{
  "error": {
    "code": "validation_error",
    "message": "The 'name' field is required.",
    "field": "name"
  }
}
```
---
HTTP Status Codes
Status Code	Meaning
`200 OK`	Request succeeded
`201 Created`	Resource created successfully
`400 Bad Request`	Invalid request — check the error message for details
`401 Unauthorized`	Missing or invalid API key
`403 Forbidden`	Valid API key but insufficient permissions
`404 Not Found`	Resource does not exist
`429 Too Many Requests`	Rate limit exceeded
`500 Internal Server Error`	FlowSync server error — contact support if this persists
---
Rate Limits
The FlowSync API enforces rate limits to ensure fair usage:
Plan	Requests per minute	Requests per day
Starter	60	10,000
Professional	300	100,000
Enterprise	1,000	Unlimited
When you exceed the rate limit, the API returns a `429 Too Many Requests`
response with a `Retry-After` header indicating when you can make the next request.
---
Pagination
Endpoints that return lists support cursor-based pagination using the
`next_cursor` parameter.
Request:
```bash
GET https://api.flowsync.io/v2/workflows?limit=20&cursor=NEXT_CURSOR_VALUE
```
Response:
```json
{
  "data": [...],
  "has_more": true,
  "next_cursor": "cursor_abc123"
}
```
Use the `next_cursor` value from the response as the `cursor` parameter in
your next request to retrieve the following page.
---
Related Topics
Authentication — How to authenticate API requests
Workflows — Workflows endpoint reference
Error Codes — Complete error code reference
