# SQL Query Troubleshooting

SQL queries are commonly used in Application and Production Support to investigate data issues, validate transactions, troubleshoot application behavior, and support root cause analysis.

## 1. Verify Query Results

Start by checking whether the expected records are available.

```sql
SELECT order_id,
       status,
       created_date
FROM orders
WHERE order_id = '10001';
```

Verify:

* Record availability
* Order status
* Creation date
* Update date
* Transaction details

## 2. Check Query Conditions

An incorrect `WHERE` condition can result in missing or unexpected records.

Example:

```sql
SELECT *
FROM orders
WHERE status = 'CONFIRMED';
```

Verify that:

* Column names are correct
* Filter values are correct
* Date conditions are correct
* Required conditions are not missing

## 3. Check NULL Values

Use `IS NULL` or `IS NOT NULL` when checking for missing values.

```sql
SELECT *
FROM orders
WHERE customer_id IS NULL;
```

Avoid using:

```sql
customer_id = NULL
```

because SQL requires `IS NULL` for NULL comparison.

## 4. Troubleshoot Date Queries

Date and time conditions can sometimes cause unexpected results.

Example:

```sql
SELECT order_id,
       created_date
FROM orders
WHERE created_date >= SYSDATE - 1
ORDER BY created_date DESC;
```

When investigating date-related issues, verify:

* Date format
* Time zone
* Date range
* Timestamp values
* Database server time

## 5. Check Joins

Incorrect joins can result in missing or duplicate records.

Example:

```sql
SELECT o.order_id,
       o.status,
       c.customer_name
FROM orders o
JOIN customers c
  ON o.customer_id = c.customer_id
WHERE o.order_id = '10001';
```

When troubleshooting joins, verify:

* Join condition
* Join type
* Matching keys
* Duplicate records
* NULL values

## 6. Check Query Performance

For slow queries, review the execution plan.

Oracle example:

```sql
EXPLAIN PLAN FOR
SELECT *
FROM orders
WHERE order_id = '10001';
```

Then:

```sql
SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY);
```

Review the execution plan for:

* Full table scans
* Index usage
* Join operations
* High-cost operations
* Large data scans

## 7. Troubleshoot Slow Queries

Possible causes include:

* Missing indexes
* Large data volume
* Inefficient joins
* Functions applied to indexed columns
* Incorrect filtering
* Blocking or locking
* High database resource utilization

Before making database changes, follow the appropriate review and approval process.

## 8. Production Support Troubleshooting Process

When a SQL-related issue is reported:

1. Understand the business issue.
2. Collect the order, transaction, or reference ID.
3. Identify the relevant database tables.
4. Run read-only queries to validate the data.
5. Check filters and joins.
6. Compare database data with application/API results.
7. Review application logs when required.
8. Investigate query performance if applicable.
9. Identify the root cause.
10. Document the findings and resolution.

## 9. Example Scenario

### Issue

A customer reports that an order is not visible in the application.

### Investigation

* Collected the order ID.
* Queried the database using the order ID.
* Confirmed whether the record exists.
* Checked the order status.
* Verified customer and transaction information.
* Compared database results with the application response.
* Reviewed application logs if required.

### Result

The investigation helps determine whether the issue is related to missing database data, incorrect application filtering, API processing, or another application component.

## 10. Production Safety

For production database troubleshooting:

* Prefer read-only `SELECT` queries.
* Do not execute `UPDATE`, `DELETE`, or structural changes without authorization.
* Follow change-management procedures.
* Take appropriate backups where required before approved changes.
* Never expose production data in GitHub.
* Never store database credentials or connection strings in the repository.
* Use sample data in documentation.

## 11. Best Practices

* Use specific filters when querying production data.
* Avoid unnecessary `SELECT *` queries on large tables.
* Use transaction or order IDs to trace issues.
* Validate SQL results against application behavior.
* Document recurring SQL issues and resolutions.
* Consider query performance during troubleshooting.
