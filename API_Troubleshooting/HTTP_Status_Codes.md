# HTTP Status Codes – API Troubleshooting

HTTP status codes help identify whether an API request was successful or whether an issue occurred during request processing.

## 1. Common HTTP Status Codes

| Status Code | Meaning               | Description                                                  |
| ----------- | --------------------- | ------------------------------------------------------------ |
| 200         | OK                    | Request completed successfully                               |
| 201         | Created               | New resource was successfully created                        |
| 202         | Accepted              | Request accepted for processing                              |
| 204         | No Content            | Request successful but no response body                      |
| 400         | Bad Request           | Invalid request or incorrect parameters                      |
| 401         | Unauthorized          | Authentication is missing or invalid                         |
| 403         | Forbidden             | Request is understood but access is not allowed              |
| 404         | Not Found             | Requested resource or endpoint does not exist                |
| 405         | Method Not Allowed    | HTTP method is not supported for the endpoint                |
| 408         | Request Timeout       | Server timed out waiting for the request                     |
| 409         | Conflict              | Request conflicts with the current resource state            |
| 429         | Too Many Requests     | Rate limit exceeded                                          |
| 500         | Internal Server Error | Server-side application error                                |
| 502         | Bad Gateway           | Gateway received an invalid response from an upstream server |
| 503         | Service Unavailable   | Service is temporarily unavailable                           |
| 504         | Gateway Timeout       | Gateway did not receive a timely response from upstream      |

## 2. Troubleshooting Approach

When an API returns an unexpected HTTP status code:

### Step 1: Check the API Endpoint

Verify that the API URL and endpoint are correct.

Example:

```text
https://api.example.com/orders
```

### Step 2: Check the HTTP Method

Confirm that the correct HTTP method is being used:

```text
GET
POST
PUT
PATCH
DELETE
```

### Step 3: Check Authentication

Verify that the required authentication method is configured correctly.

Common methods include:

* API Key
* Bearer Token
* Basic Authentication
* OAuth

Never store real API keys, passwords, or tokens in GitHub.

### Step 4: Check Request Headers

Review headers such as:

```text
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
```

### Step 5: Validate Request Body

For POST, PUT, and PATCH requests, verify that the JSON or XML request body contains the required fields and correct data types.

Example:

```json
{
  "orderId": "10001",
  "status": "CONFIRMED"
}
```

### Step 6: Check the Response

Review:

* HTTP status code
* Response body
* Error message
* Response headers
* Response time

### Step 7: Check Application Logs

If the API returns a **4xx or 5xx error**, check the application logs for additional information.

Useful Linux commands:

```bash
tail -100 application.log
grep -i "error" application.log
grep -i "exception" application.log
```

### Step 8: Test Using Postman

Use Postman to reproduce the issue and verify:

* Endpoint
* HTTP method
* Headers
* Authentication
* Request body
* Response
* Status code

## 3. Example Troubleshooting

### Issue

API returns:

```text
HTTP 401 Unauthorized
```

### Possible Causes

* Invalid or expired token
* Missing Authorization header
* Incorrect API credentials
* Authentication configuration issue

### Investigation

1. Verify the Authorization header.
2. Check whether the token is valid.
3. Confirm the API authentication method.
4. Check application/API logs.
5. Re-test the request using Postman.

### Resolution

Correct the authentication configuration or obtain a valid authentication token, then retest the API.

## 4. Production Support Best Practices

* Always verify the issue before making changes.
* Check application logs and API responses.
* Validate the request and response payloads.
* Use transaction/order IDs to trace requests.
* Follow change-management procedures for production changes.
* Do not expose passwords, API keys, tokens, customer data, or production credentials.
* Document the root cause and resolution after resolving the incident.
