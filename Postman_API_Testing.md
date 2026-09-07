# Postman API Testing

Postman is used to test, validate, and troubleshoot REST APIs by sending requests and analyzing API responses.

## 1. API Testing Using Postman

Postman can be used to validate:

* API endpoints
* HTTP methods
* Request headers
* Authentication
* Request parameters
* JSON/XML request bodies
* HTTP status codes
* API responses
* Response time

## 2. Common HTTP Methods

### GET

Used to retrieve information from an API.

Example:

```text
GET /orders/10001
```

### POST

Used to create a new record or resource.

Example:

```text
POST /orders
```

### PUT

Used to update an existing resource.

Example:

```text
PUT /orders/10001
```

### PATCH

Used to partially update an existing resource.

Example:

```text
PATCH /orders/10001
```

### DELETE

Used to delete a resource.

Example:

```text
DELETE /orders/10001
```

## 3. Request Validation

Before sending an API request, verify:

* API endpoint
* HTTP method
* Authentication
* Headers
* Query parameters
* Path parameters
* Request body

Example JSON request:

```json
{
  "orderId": "10001",
  "status": "CONFIRMED",
  "quantity": 2
}
```

## 4. Request Headers

Common API headers include:

```text
Content-Type: application/json
Accept: application/json
Authorization: Bearer <token>
```

Never store real passwords, API keys, access tokens, or credentials in GitHub.

## 5. Authentication Testing

Common authentication methods include:

* API Key
* Bearer Token
* Basic Authentication
* OAuth 2.0

When troubleshooting authentication issues, verify:

1. Authentication method
2. Token/API key validity
3. Authorization header
4. Token expiration
5. Required permissions

## 6. Response Validation

After sending the request, validate:

* HTTP status code
* Response body
* Response headers
* Response time
* Error messages
* Expected data

Example successful response:

```json
{
  "orderId": "10001",
  "status": "CONFIRMED"
}
```

## 7. Common API Errors

### 400 – Bad Request

Possible causes:

* Missing mandatory fields
* Invalid JSON
* Incorrect parameter values
* Invalid data format

### 401 – Unauthorized

Possible causes:

* Missing authentication
* Invalid token
* Expired token

### 403 – Forbidden

Possible causes:

* Insufficient permissions
* User/service account does not have required access

### 404 – Not Found

Possible causes:

* Incorrect endpoint
* Invalid resource ID
* Resource does not exist

### 500 – Internal Server Error

Possible causes:

* Application error
* Database issue
* Unexpected server-side exception

## 8. API Troubleshooting Process

When an API fails:

1. Reproduce the issue using Postman.
2. Verify the endpoint and HTTP method.
3. Check authentication and headers.
4. Validate the request payload.
5. Review the HTTP status code.
6. Analyze the response message.
7. Check application logs.
8. Verify backend/database data where required.
9. Identify the root cause.
10. Retest after the issue is resolved.

## 9. Production Support Example

### Issue

An order API is returning:

```text
HTTP 500 Internal Server Error
```

### Investigation

* Reproduced the issue using Postman.
* Verified the API endpoint and HTTP method.
* Checked request headers and JSON payload.
* Reviewed the API response.
* Checked application logs using the transaction/order ID.
* Verified related backend data using SQL.
* Identified the source of the application error.

### Resolution

After the issue was corrected, the API was retested using Postman and the expected successful response was received.

## 10. Best Practices

* Use sample/test data for documentation.
* Never commit credentials or sensitive information to GitHub.
* Maintain separate environments for development, testing, and production.
* Validate both positive and negative API scenarios.
* Record HTTP status codes and error messages during troubleshooting.
* Use unique transaction/order IDs to trace requests.
* Document the root cause and resolution for recurring issues.
