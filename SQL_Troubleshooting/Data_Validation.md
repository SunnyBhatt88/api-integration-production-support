# SQL Data Validation

SQL is commonly used in Application and Production Support to validate backend data, investigate transaction issues, and identify data-related problems.

## 1. Basic Data Validation

Use SELECT queries to verify whether the expected records are available.

Example:

```sql
SELECT *
FROM orders
WHERE order_id = '10001';
```

Check:

* Record availability
* Order status
* Customer information
* Transaction details
* Creation and update timestamps

## 2. Check Specific Columns

Instead of retrieving all columns, select only the required fields.

```sql
SELECT order_id,
       status,
       created_date,
       updated_date
FROM orders
WHERE order_id = '10001';
```

This makes investigation easier and reduces unnecessary data retrieval.

## 3. Check Record Count

Use COUNT to verify the number of records.

```sql
SELECT COUNT(*)
FROM orders
WHERE order_id = '10001';
```

This can help identify missing or duplicate records.

## 4. Check for Duplicate Records

Example:

```sql
SELECT order_id,
       COUNT(*) AS record_count
FROM orders
GROUP BY order_id
HAVING COUNT(*) > 1;
```

This can help identify duplicate records that may affect order processing or integrations.

## 5. Check NULL Values

Identify records where important fields are missing.

```sql
SELECT *
FROM orders
WHERE status IS NULL;
```

NULL checks are useful when investigating incomplete transactions or failed processing.

## 6. Validate Order Status

Example:

```sql
SELECT order_id,
       status
FROM orders
WHERE order_id = '10001';
```

Verify whether the database status matches the expected application or API status.

## 7. Check Recent Transactions

Example:

```sql
SELECT order_id,
       status,
       created_date
FROM orders
WHERE created_date >= SYSDATE - 1
ORDER BY created_date DESC;
```

This can be useful for investigating recent production transactions.

## 8. Troubleshooting Process

When investigating a production issue:

1. Collect the transaction, order, or reference ID.
2. Identify the relevant database table.
3. Run a SELECT query to validate the record.
4. Check the transaction status.
5. Verify required fields.
6. Check for duplicate or missing records.
7. Compare database information with application/API responses.
8. Review application logs when required.
9. Identify the root cause.
10. Document the findings and resolution.

## 9. Example Production Support Scenario

### Issue

An order is successfully created through an API, but the expected status is not displayed in the application.

### Investigation

* Collected the order ID from the incident.
* Checked the order record using SQL.
* Verified the current database status.
* Checked related transaction information.
* Compared the database status with the API response.
* Reviewed application logs to identify processing issues.

### Result

The investigation helped identify whether the issue was related to database data, API processing, or application behavior.

## 10. Production Safety

When working with production databases:

* Use SELECT queries for investigation unless a change is specifically authorized.
* Never execute UPDATE or DELETE statements without proper approval.
* Follow change-management procedures.
* Do not expose customer or production data in GitHub.
* Never store database usernames, passwords, connection strings, or credentials in repositories.
* Use sample data when documenting troubleshooting examples.
