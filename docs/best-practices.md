Best Practices
Follow these best practices to build reliable, maintainable workflows with
the FlowSync API.
---
API Key Management
Use one API key per integration. Create a separate API key for each
application or environment that accesses FlowSync. This makes it easy to
revoke a single integration's access without affecting others.
Store API keys as environment variables. Never hardcode API keys in
your source code or commit them to version control.
```bash
# Store the key as an environment variable
export FLOWSYNC_API_KEY="your_api_key_here"
```
Use the minimum required scope. If your integration only reads data,
use a Read Only key. Only use Admin-scoped keys when workspace-level
operations are required.
---
Handling Rate Limits
Implement exponential backoff. When you receive a `429 Too Many Requests`
error, wait for the duration specified in the `Retry-After` header before
retrying. If retries continue to fail, double the wait time with each retry.
Monitor the rate limit headers. Check `X-RateLimit-Remaining` in your
responses to track usage before you hit the limit.
---
Error Handling
Always handle errors explicitly. Check the HTTP status code and the
`error.code` field in every API response. Do not assume requests succeed.
Log error responses. Save the full error response body when errors occur.
The `error.code` and `error.message` fields are essential for debugging.
Distinguish between retryable and non-retryable errors. Server errors
(`5xx`) are typically temporary and safe to retry. Client errors (`4xx`) usually
require a code change and should not be retried automatically.
---
Workflow Design
Give workflows descriptive names. A workflow named "Send welcome email
to new customers" is easier to manage than "Workflow 1." Use names that
describe what the workflow does and when it runs.
Start workflows as drafts. Create new workflows with `"status": "draft"`
while you are still configuring triggers and steps. Change the status to
`"active"` only when the workflow is ready.
Test before activating. Use the FlowSync test trigger feature to
manually fire a workflow before setting it to active in production.
---
Related Topics
Authentication — API key setup and security
Error Codes — Complete error reference
API Overview — Rate limits and request format
