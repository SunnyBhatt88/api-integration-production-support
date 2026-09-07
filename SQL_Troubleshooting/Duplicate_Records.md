# Duplicate Records Troubleshooting

Duplicate records can cause issues such as duplicate orders, incorrect reporting, repeated transactions, and integration failures.

## 1. Identify Duplicate Records

Use `GROUP BY` and `HAVING` to identify duplicate values.

```sql
SELECT order_id,
       COUNT(*) AS record_count
FROM orders
GROUP BY order_id
HAVING COUNT(*) > 1;
```

## 2. Investigate a Specific Order

Once a duplicate order ID is identified, retrieve the related records.

```sql
SELECT *
FROM orders
WHERE order_id = '10001'
ORDER BY created_date;
```

Check:

* Order ID
* Status
* Created date
* Updated date
* Transaction/reference ID
* Source system
* Processing status

## 3. Check Duplicate Transactions

Example:

```sql
SELECT transaction_id,
       COUNT(*) AS record_count
FROM transactions
GROUP BY transaction_id
HAVING COUNT(*) > 1;
```

This can help identify repeated transaction processing.

## 4. Investigate Duplicate API Requests

When an API request appears to have been processed more than once:

1. Identify the transaction/order ID.
2. Check application logs.
3. Check API request and response details.
4. Search the database for duplicate records.
5. Compare timestamps.
6. Check whether the same request was submitted multiple times.
7. Identify the source of the duplicate processing.

## 5. Common Causes

Possible causes include:

* Duplicate API requests
* Retry mechanism issues
* Network timeout followed by request retry
* Application processing errors
* Missing idempotency controls
* Incorrect integration logic
* Batch job reprocessing
* Manual duplicate submissions

## 6. Production Support Approach

When a duplicate record issue is reported:

1. Collect the order or transaction ID.
2. Verify the issue in the database.
3. Review application logs.
4. Check API request/response information.
5. Identify when and how the duplicate was created.
6. Determine the root cause.
7. Follow the appropriate approval process before making any data correction.
8. Document the incident and resolution.

## 7. Production Safety

Do not directly delete duplicate production records without proper authorization.

Avoid executing statements such as:

```sql
DELETE FROM orders
WHERE order_id = '10001';
```

unless the change has been properly reviewed and approved.

For production investigations, prefer read-only queries such as `SELECT`.

## 8. Best Practices

* Use unique transaction or order IDs for investigation.
* Check application logs along with database records.
* Compare timestamps to understand processing sequence.
* Verify API retry behavior.
* Document the root cause.
* Follow change-management procedures.
* Never include real customer or production data in GitHub.
