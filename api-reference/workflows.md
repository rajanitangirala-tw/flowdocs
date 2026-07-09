Workflows
Workflows are the core building blocks of FlowSync. A workflow defines a
sequence of steps that run automatically when a trigger fires. Use the
Workflows API to create, retrieve, update, and delete workflows.
---
Endpoints
Method	Endpoint	Description
GET	`/v2/workflows`	List all workflows in your workspace
POST	`/v2/workflows`	Create a new workflow
GET	`/v2/workflows/{workflow_id}`	Retrieve a specific workflow
PUT	`/v2/workflows/{workflow_id}`	Update a workflow
DELETE	`/v2/workflows/{workflow_id}`	Delete a workflow
---
List All Workflows
Retrieves a paginated list of all workflows in your workspace.
Request
```bash
GET https://api.flowsync.io/v2/workflows
```
Query Parameters
Parameter	Type	Required	Description
`status`	string	No	Filter by status: `active`, `inactive`, or `draft`
`limit`	integer	No	Number of results to return. Default: 20. Maximum: 100
`cursor`	string	No	Cursor for pagination. Use the `next_cursor` from the previous response
Example Request
```bash
curl -X GET "https://api.flowsync.io/v2/workflows?status=active&limit=10" \
  -H "Authorization: Bearer YOUR_API_KEY"
```
Example Response
```json
{
  "data": [
    {
      "workflow_id": "wf_01abc123",
      "name": "Daily Report",
      "status": "active",
      "step_count": 3,
      "created_at": "2026-06-01T09:00:00Z",
      "updated_at": "2026-06-15T14:30:00Z"
    },
    {
      "workflow_id": "wf_02xyz456",
      "name": "Weekly Digest",
      "status": "active",
      "step_count": 5,
      "created_at": "2026-06-10T11:00:00Z",
      "updated_at": "2026-07-01T10:00:00Z"
    }
  ],
  "has_more": false,
  "next_cursor": null
}
```
---
Create a Workflow
Creates a new workflow in your workspace.
Request
```bash
POST https://api.flowsync.io/v2/workflows
```
Request Body Parameters
Parameter	Type	Required	Description
`name`	string	Yes	The workflow name. Maximum 100 characters
`description`	string	No	A description of what the workflow does. Maximum 500 characters
`status`	string	No	Initial status: `active` or `draft`. Default: `draft`
Example Request
```bash
curl -X POST https://api.flowsync.io/v2/workflows \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Customer Onboarding",
    "description": "Sends welcome emails and creates CRM records for new customers",
    "status": "active"
  }'
```
Example Response
```json
{
  "workflow_id": "wf_03def789",
  "name": "Customer Onboarding",
  "description": "Sends welcome emails and creates CRM records for new customers",
  "status": "active",
  "step_count": 0,
  "created_at": "2026-07-01T15:00:00Z",
  "updated_at": "2026-07-01T15:00:00Z"
}
```
Result: A `201 Created` response confirms the workflow was created.
Note the `workflow_id` — you will use it to add triggers and steps.
---
Retrieve a Workflow
Retrieves the details of a specific workflow.
Request
```bash
GET https://api.flowsync.io/v2/workflows/{workflow_id}
```
Path Parameters
Parameter	Type	Required	Description
`workflow_id`	string	Yes	The ID of the workflow to retrieve
Example Request
```bash
curl -X GET https://api.flowsync.io/v2/workflows/wf_03def789 \
  -H "Authorization: Bearer YOUR_API_KEY"
```
Example Response
```json
{
  "workflow_id": "wf_03def789",
  "name": "Customer Onboarding",
  "description": "Sends welcome emails and creates CRM records for new customers",
  "status": "active",
  "step_count": 2,
  "created_at": "2026-07-01T15:00:00Z",
  "updated_at": "2026-07-02T09:00:00Z"
}
```
---
Update a Workflow
Updates the name, description, or status of an existing workflow.
Request
```bash
PUT https://api.flowsync.io/v2/workflows/{workflow_id}
```
Request Body Parameters
Parameter	Type	Required	Description
`name`	string	No	The new workflow name
`description`	string	No	The new workflow description
`status`	string	No	The new status: `active`, `inactive`, or `draft`
Example Request
```bash
curl -X PUT https://api.flowsync.io/v2/workflows/wf_03def789 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "status": "inactive"
  }'
```
Example Response
```json
{
  "workflow_id": "wf_03def789",
  "name": "Customer Onboarding",
  "status": "inactive",
  "updated_at": "2026-07-03T10:00:00Z"
}
```
---
Delete a Workflow
Permanently deletes a workflow and all its associated steps and triggers.
Request
```bash
DELETE https://api.flowsync.io/v2/workflows/{workflow_id}
```
> **Note:** Deleting a workflow is permanent and cannot be undone. Active
> workflow runs in progress are not interrupted, but no new runs will start.
Example Request
```bash
curl -X DELETE https://api.flowsync.io/v2/workflows/wf_03def789 \
  -H "Authorization: Bearer YOUR_API_KEY"
```
Example Response
A successful delete returns a `204 No Content` response with an empty body.
---
Related Topics
Triggers — Add triggers to start your workflows automatically
Error Codes — Handle workflow API errors
