**Expensify Postman Collection Glossary**

This table defines key terms you will encounter throughout the Expensify API.

| Term | Definition | Usage in Expensify Collection |
| --- | --- | --- |
| API (Application Programming Interface) | A set of commands, functions, protocols, and objects that expose functionalities of an application or service to software developers. | This collection uses the Expensify API to interact with data and functionalities. |
| Authentication | The process of verifying a user's identity to grant access to a system or resource. | The collection uses API credentials (partnerUserID and partnerUserSecret) for authentication within your Postman requests. |
| Authorization | The process of determining what actions a user is allowed to perform after successful authentication. | Expensify API controls access based on the permissions associated with your credentials. |
| Collection (Postman) | A group of related API requests organized together within Postman. | This collection contains requests for various Expensify API functionalities (specific functionalities to be listed based on the collection's purpose). |
| Endpoint | A specific URL that represents a resource or functionality within the Expensify API. | You'll use different endpoints for various actions like downloading reports (specific endpoints with brief descriptions can be listed). |
| Environment (Postman) | A set of key-value pairs that represent environment variables. | You can use environments to store reusable values like API credentials or base URLs (specific use cases for environments within the collection can be mentioned). |
| Error Code | A numeric code included in the API response that indicates whether the request was successful (e.g., 200 OK) or encountered an error (e.g., 404 Not Found). | This collection likely includes descriptions for common Expensify API error codes. |
| FTL | FreeMarker Template Language | Expensify supports FTL for generating custom report outputs, |
| POST (HTTP Method) | An HTTP method used to send data to a server to create or update resources. | The collection uses POST requests for actions that modify data, such as creating reports or updating their status. |
| JSON (JavaScript Object Notation) | A lightweight data interchange format commonly used to represent structured data in API requests and responses. | Expensify uses JSON for data exchange in requests and responses. |
| OAuth | An authorization framework that allows users to grant third-party applications access to their accounts without sharing their credentials directly. |  |
| Partner User ID & Partner User Secret | The API credentials you generate from your Expensify account to access the Expensify API. These are required for authentication in your Postman requests. |  |
| Postman | A popular application for building, testing, and managing API requests. | This Expensify collection is designed to be used within Postman. |
| Query Parameter | Key-value pairs appended to the URL of an API request to filter or modify its behavior. | Expensify might use query parameters for filtering reports based on dates or other criteria (specific examples can be listed). |
| Request | An HTTP message sent to a server to initiate communication and request a specific action or data. | This collection consists of various POST requests tailored for interacting with the Expensify API. |
| Response | The HTTP message sent back by the server in response to a request. It contains data or a status code indicating the outcome of the request. |  |
| Resource | An entity or piece of data managed by the Expensify API, such as reports, users, or expense categories. | The collection interacts with various Expensify resources (specific resources the collection interacts with can be listed). |
| REST (Representational State Transfer) | An architectural style for designing APIs that emphasizes using a standardized set of HTTP methods (GET, POST, PUT, DELETE) to interact with resources. | Expensify utilizes a RESTful API. |