# BigDataSpark — лабораторная №2

Запуск пайплайна:

```powershell
cd путь\к\BigDataSpark-main
.\run.ps1
```

---

### PostgreSQL

```sql
SELECT COUNT(*) FROM staging.mock_data;

SELECT COUNT(*) FROM dw.fact_sales;

SELECT COUNT(*) FROM dw.dim_date;
SELECT COUNT(*) FROM dw.dim_customer;
SELECT COUNT(*) FROM dw.dim_product;
SELECT COUNT(*) FROM dw.dim_seller;
SELECT COUNT(*) FROM dw.dim_store;
SELECT COUNT(*) FROM dw.dim_supplier;

\dt dw.*

SELECT f.sale_id, d.full_date, c.first_name, p.product_name, f.sale_total_price
FROM dw.fact_sales f
JOIN dw.dim_date d ON f.date_key = d.date_key
JOIN dw.dim_customer c ON f.customer_key = c.customer_key
JOIN dw.dim_product p ON f.product_key = p.product_key
LIMIT 10;
```

---

### ClickHouse

```sql
SHOW TABLES FROM labdb;

SELECT name, total_rows
FROM system.tables
WHERE database = 'labdb' AND name LIKE 'mart_%';

SELECT generated_at, length(top10_products), length(revenue_by_category)
FROM labdb.mart_product_sales
ORDER BY generated_at DESC
LIMIT 1;
```

```sql
SELECT name
FROM system.tables
WHERE database = 'labdb'
  AND name IN (
    'mart_product_sales',
    'mart_customer_sales',
    'mart_time_sales',
    'mart_store_sales',
    'mart_supplier_sales',
    'mart_product_quality'
  )
ORDER BY name;
```
