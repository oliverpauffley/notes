# Materialized Views
They are a way of saving a regular view's results so that you don't need to repeat the query.

- It behaves like a table.
- use to cache slow query results. 
- must be refreshed.
- Be careful to use CONCURRENTLY to avoid locks.
-  you must have a unique index. 

## Example
```sql
CREATE MATERIALIZED VIEW sales_summary AS
  SELECT
      seller_no,
      invoice_date,
      sum(invoice_amt)::numeric(13,2) as sales_amt
    FROM invoice
    WHERE invoice_date < CURRENT_DATE
    GROUP BY
      seller_no,
      invoice_date
    ORDER BY
      seller_no,
      invoice_date;

CREATE UNIQUE INDEX sales_summary_seller
  ON sales_summary (seller_no, invoice_date);
  ```
  
  ```sql
  REFRESH MATERIALIZED VIEW CONCURRENTLY sales_summary
  ```