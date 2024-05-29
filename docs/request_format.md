Every request to the Expensify API follows the same pattern: a JSON payload that identifies the job to execute is passed as a parameter called `requestJobDescription`. Additionally, other parameters may be needed based on the type of job.

Finally, there is a general rate limit of 50 jobs started per minute. Exceeding this limit will result in the following error message: `You have been rate-limited. Please try again later or contact help@expensify.com for assistance.`

Every request has to be made against the endpoint `https://integrations.expensify.com/Integration-Server/ExpensifyIntegrations`.

**Request Job Description format**

For every request, the `requestJobDescription` JSON parameter needs to contain the following data:

| PARAMETER | TYPE | DESCRIPTION |
| --- | --- | --- |
| type | String | The type of job to execute. |
| credentials | JSON object | An object containing two key-values used to authenticate you:  <br>\* partnerUserID |
|  |  | \* partnerUserSecret |
| inputSettings | JSON Object | (Optional) Additional settings specific to the job type. Refer to the Expensify API documentation for details on supported inputSettings for each job. |