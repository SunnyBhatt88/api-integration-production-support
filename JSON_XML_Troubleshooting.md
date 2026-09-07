# JSON & XML Troubleshooting

JSON and XML are commonly used data formats for exchanging information between applications and APIs.

## 1. JSON

JSON (JavaScript Object Notation) is a lightweight format commonly used in REST APIs.

Example:

```json
{
  "orderId": "10001",
  "customer": "Test Customer",
  "status": "CONFIRMED",
  "quantity": 2
}
```

## 2. XML

XML (Extensible Markup Language) is another format used for exchanging structured data between applications.

Example:

```xml
<Order>
    <OrderId>10001</OrderId>
    <Customer>Test Customer</Customer>
    <Status>CONFIRMED</Status>
    <Quantity>2</Quantity>
</Order>
```

## 3. Common JSON Issues

### Invalid JSON Syntax

Common causes:

* Missing comma
* Missing quotation marks
* Incorrect brackets
* Incorrect data types
* Duplicate or incorrectly named fields

Example of incorrect JSON:

```json
{
  "orderId": "10001"
  "status": "CONFIRMED"
}
```

The comma between `orderId` and `status` is missing.

Correct version:

```json
{
  "orderId": "10001",
  "status": "CONFIRMED"
}
```

## 4. Common XML Issues

Common causes:

* Missing closing tags
* Incorrect nesting
* Invalid characters
* Incorrect element names
* Missing required elements

Example:

```xml
<Order>
    <OrderId>10001</OrderId>
    <Status>CONFIRMED</Status>
</Order>
```

Always verify that XML opening and closing tags are properly matched.

## 5. API Payload Validation

When troubleshooting API payload issues, verify:

1. Request format
2. Required fields
3. Field names
4. Data types
5. Mandatory values
6. Special characters
7. Content-Type header

Common headers:

```text
Content-Type: application/json
Accept: application/json
```

For XML:

```text
Content-Type: application/xml
```

## 6. Troubleshooting Using Postman

Postman can be used to validate JSON and XML payloads.

Check:

* Request body
* Headers
* Authentication
* Response status code
* Response body
* Error message

For JSON requests, select:

**Body → raw → JSON**

For XML requests, select:

**Body → raw → XML**

## 7. Common API Payload Errors

### HTTP 400 – Bad Request

Possible causes:

* Invalid JSON/XML
* Missing mandatory field
* Incorrect field name
* Invalid data type
* Incorrect request format

### HTTP 415 – Unsupported Media Type

Possible cause:

The `Content-Type` header does not match the request payload.

Example:

```text
Content-Type: application/json
```

when the API expects XML.

### HTTP 422 – Unprocessable Entity

Possible causes:

* Valid JSON/XML but invalid business data
* Incorrect field value
* Business validation failure
* Missing required business information

## 8. Production Troubleshooting Process

When an API payload fails:

1. Reproduce the issue using Postman.
2. Check the HTTP status code.
3. Validate the JSON/XML syntax.
4. Verify required fields.
5. Check field names and data types.
6. Verify request headers.
7. Review the API response.
8. Search application logs using the transaction/order ID.
9. Validate backend data using SQL when required.
10. Document the root cause and resolution.

## 9. Example Troubleshooting Scenario

### Issue

An order API returns:

```text
HTTP 400 Bad Request
```

### Investigation

* Reproduced the request in Postman.
* Reviewed the JSON request body.
* Identified a missing mandatory field.
* Verified the expected payload structure.
* Corrected the request payload.
* Retested the API.

### Result

The API successfully processed the request after the payload was corrected.

## 10. Best Practices

* Validate JSON/XML before sending API requests.
* Always verify the `Content-Type` header.
* Check mandatory fields and expected data types.
* Use transaction IDs for troubleshooting.
* Use sample data when documenting examples.
* Never include customer data, credentials, tokens, or confidential production information in GitHub.
* Document recurring payload issues and their resolutions.
