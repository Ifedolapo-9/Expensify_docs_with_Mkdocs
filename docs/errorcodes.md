**Expensify API Error Codes**

This table lists potential error codes encountered when using the Expensify API and their possible reasons.

| Error Code | Possible Reason |
| --- | --- |
| 207 (Partial Success) | Some of the reports failed to update. Their IDs are contained in the list `failedReports` within the response. |
| 400 (Bad Request) | Missing required parameter |
|  | Invalid parameter value format |
|  | Malformed JSON body |
| 401 (Unauthorized) | Invalid or missing API credentials |
|  | Insufficient permissions for the requested action |
| 403 (Forbidden) | The requested action is not allowed for your account |
|  | Resource access restrictions in place |
| 404 (Not Found) | Requested endpoint does not exist |
|  | Resource not found (e.g., report with a specific ID) |
| 409 (Conflict) | Attempting to create a duplicate resource (e.g., creating a report with an existing ID) |
|  | Conflicting data in the request |
| 410 (Validation Error) | The request contains invalid data that fails validation checks on the Expensify API side. |
|  | Examples: Malformed date format, invalid enum value, etc. |
| 410 (Gone) | Requested endpoint has been deprecated and is no longer available |
|  | Resource has been deleted |
| 422 (Unprocessable Entity) | Validation errors in the request payload |
|  | Business logic violation (e.g., attempting to update a report with an invalid status) |
| 429 (Too Many Requests) | Exceeding API rate limits |
|  | Throttling applied due to frequent requests |
| 500 (Generic Error) | Unexpected error on the Expensify API server. |
|  | This is a generic error code for internal server issues. Consult Expensify support for further investigation in case of a 500 error. |