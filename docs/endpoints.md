# Expensify Endpoints

## EXPORT

Export expense or report data in a configurable format for analysis or insertion into your accounting package. See the [export template format reference](https://integrations.expensify.com/Integration-Server/doc/export_report_template.html) for more information about how to write export templates.

***`requestJobDescription` format***

| NAME | FORMAT | VALID VALUES | DESCRIPTION |
| --- | --- | --- | --- |
| type | String | file |  |
| onReceive | JSON object | `{"immediateResponse":["returnRandomFileName"]}` | Returns the name of the generated report. Only this export mode is supported at the moment. |
| inputSettings | JSON object | See inputSettings | Settings used to filter the reports that are exported. |
| outputSettings | JSON object | See outputSettings | Settings for the generated file. |
| **Optional elements** |  |  |  |
| test | String | true, false | If set to true, actions defined in `onFinish` will not be executed. |
| onFinish | JSON array | See onFinish | Actions performed at the end of the export. |

- `inputSettings`
    

| NAME | FORMAT | VALID VALUES | DESCRIPTION |
| --- | --- | --- | --- |
| type | String | combinedReportData | Specifies all Expensify reports will be combined into a single file. |
| filters | JSON object | See inputSettings filters |  |
| **Optional elements** |  |  |  |
| reportState | String | One or more of `"OPEN"`, `"SUBMITTED"`, `"APPROVED"`, `"REIMBURSED"`, `"ARCHIVED"`.  <br>When using multiple statuses, separate them by a comma, _e.g._ `"APPROVED,REIMBURSED"`  <br>**Note:** These values respectively match the statuses "Open", "Processing", "Approved", "Reimbursed" and "Closed" on the website | Only the reports matching the specified status(es) will be exported. |
| limit | String | Any integer, as a string | Maximum number of reports to export. |
| employeeEmail | String | A valid email address  <br>**Note:**  <br>\* The usage of this parameter is restricted to certain domains  <br>\* If this parameter is used, reports in the OPEN status cannot be exported | The reports will be exported from that account. |

- `inputSettings.filters`
    

| NAME | FORMAT | VALID VALUES | DESCRIPTION |
| --- | --- | --- | --- |
| reportIDList | String,  <br>_Required if_ `_startDate_` _or_ `_approvedAfter_` _are not specified_ |  | Comma-separated list of report IDs to be exported. |
| policyIDList | String,  <br>_Optional_ |  | Comma-separated list of policy IDs the exported reports must be under. |
| startDate | Date,  <br>_Required if_ `_reportIDList_` _or_ `_approvedAfter_` _are not specified_ | yyyy-mm-dd formatted date | Filters out all reports submitted or created before the given date, whichever occurred last (inclusive). |
| endDate | Date,  <br>_Optional_ | yyyy-mm-dd formatted date | Filters out all reports submitted or created after the given date, whichever occurred last (inclusive). |
| approvedAfter | Date,  <br>_Required if_ `_reportIDList_` _or_ `_startDate_` _are not specified_ | yyyy-mm-dd formatted date | Filters out all reports approved before, or on that date. This filter is only used against reports that have been approved. |
| markedAsExported | String,  <br>_Optional_ | Any string | Filters out reports that have already been exported with that label out. |

- `outputSettings`
    

| NAME | FORMAT | VALID VALUES | DESCRIPTION |
| --- | --- | --- | --- |
| fileExtension | String | One or multiple of "csv", "xls", "xlsx", "txt", "pdf", "json", "xml" | Specifies the format of the generated report.  <br>_Note_: if the "pdf" option is chosen, one PDF file will be generated for each report exported. |
| **Optional elements** |  |  |  |
| fileBasename | String | Any valid file base name | The name of the generated file(s) will start with this value, and a random part will be added to make each filename globally unique. If not specified, the default value `export` is used. |
| includeFullPageReceiptsPdf | Boolean | `true`, `false` | Specifies whether generated PDFs should include full page receipts. This parameter is used only if `fileExtension` contains `pdf`. |

- `onFinish` (Optional)
    

This section can be used to describe actions that need to be performed at the end of the export.

| ACTION NAME | DESCRIPTION |
| --- | --- |
| email | Send an email linking to the generated report to a provided list of recipients. |
| markAsExported | Mark the exported reports as “Exported” in Expensify. |
| sftpUpload | upload the generated file(s) to an SFTP server. |

| NAME | FORMAT | VALID VALUES | DESCRIPTION |
| --- | --- | --- | --- |
| **`email`** action |  |  |  |
| recipients | String | Comma-separated list of valid email addresses | People to email at the end of the export. |
| message | String | Plain text or Freemarker message | Content of the message. If using Freemarker, the `filenames` list can be used to get the names of all files that have been generated. |
| **`markAsExported`** action |  |  |  |
| label | String | Any string value | The exported reports will be marked as exported with this label. |
| **`sftpUpload`** action |  |  |  |
| sftpData | JSON object |  | See below |
| **`sftpUpload.sftpData`** action |  |  |  |
| host | String |  | The SFTP host to connect to. You can upload to a specific folder by setting the `homedir` (home directory) of the SFTP user to that folder. You cannot specify a specific folder any other way. |
| login | String |  | The username to use for SFTP authentication. |
| password | String |  | The password to use during authentication. |
| port | Integer |  | The port to connect to on the SFTP server. |

**Template parameter**

The `template` parameter is used to format the Expensify data as you wish. It is based on the Freemarker language's syntax.

See the [export template format reference](https://integrations.expensify.com/Integration-Server/doc/export_report_template.html) for more information about how to write export templates.

We recommend storing your template in separate files, which can be passed to the request more easily with cURL's \`@\` operator.

**Example Request**

        curl --location 'https://integrations.expensify.com/Integration-Server/ExpensifyIntegrations' \
        --data-urlencode 'requestJobDescription={
                "type":"file",
                "credentials":{
                    "partnerUserID":{{partnerUserID}},
                    "partnerUserSecret":{{partnerUserSecret}}
                },
                "onReceive":{
                    "immediateResponse":["returnRandomFileName"]
                },
                "inputSettings":{
                    "type":"combinedReportData",
                    "filters":{
                        "reportIDList": "R00bCluvcO4T,R006AseGxMka"
                    }
                },
                "outputSettings":{
                    "fileExtension":"csv"
                }
            }'\'' \
            --data-urlencode '\''template@expensify_template.ftl'\'''



**Example Response**

        {
        "responseCode": 200
        }

## CREATE

This section details creating a report within a user's Expensify account using the `requestJobDescription` format. However, this functionality requires prior enablement by Expensify Concierge.

**Requirements:**

- Domain and Policy Admin permissions
    
- Functionality enabled for your domain by contacting [concierge@expensify.com](https://mailto:concierge@expensify.com)
    

**Error Handling:**

If you encounter the "Not authorized to authenticate as user" error, it signifies report creation functionality is not enabled for your domain.

**Request Format:**

The request utilizes the `requestJobDescription` format with specific `inputSettings`. Here's a breakdown of the required fields:

| Field Name | Format | Valid Values | Description |
| --- | --- | --- | --- |
| **type** | String | "report" | Specifies the job type as report creation. |
| **employeeEmail** | String | A valid email address | The report will be created in the corresponding user's account. |
| **report** (JSON Object) |  | See report details below. | Defines report properties. |
| **expenses** (JSON Array) |  | See expenses details below. | Defines expense details to be included in the report (optional). |
| **policyID** | String | Any valid Expensify policy ID | The report will be associated with this policy. |

**inputSettings.report Details:**

| Field Name | Format | Valid Values | Description |
| --- | --- | --- | --- |
| **title** | String |  | The title of the report. |
| **fields** (Optional - JSON Object) |  | A series of key-value pairs. | Defines values for custom fields on the specified policy (key names require underscores for non-alphanumeric characters). |

**inputSettings.expenses Details (Optional):**

| Field Name | Format | Valid Values | Description |
| --- | --- | --- | --- |
| **merchant** | String |  | The merchant name for the expense. |
| **currency** | String | Three-letter currency code (e.g., USD, EUR) | The currency in which the expense was made. |
| **date** | Date | yyyy-mm-dd format | The date of the expense. |
| **amount** | Integer |  | The expense amount in cents. |

**Example Request**

        curl --location 'https://integrations.expensify.com/Integration-Server/ExpensifyIntegrations' \
        --header 'Content-Type: application/x-www-form-urlencoded' \
        --data-urlencode 'requestJobDescription={
                "type": "create",
                "credentials": {
                    "partnerUserID": {{partnerUserID}},
                    "partnerUserSecret":{{partnerUserSecret}}
                },
                "inputSettings": {
                    "type": "report",
                    "policyID": "952DB91B963583C7",
                    "report": {
                        "title": "Name of the report",
                        "fields":{
                            "reason_of_trip": "Business trip",
                            "employees": "3"
                        }
                    },
                    "employeeEmail": "ifedolapo387@gmail.com",
                    "expenses": [
                        {
                            "date": "2024-03-24",
                            "currency": "USD",
                            "merchant": "Name of merchant",
                            "amount": 1234
                        },
                        {
                            "date": "2024-03-27",
                            "currency": "CAD",
                            "merchant": "Name of merchant",
                            "amount": 2211
                        }
                    ]
                }
            }'\'''

**Example Response**

        {
    "responseCode": 200,
    "reportName": "Name of the report",
    "reportID": "R006AseGxMka"
    }




