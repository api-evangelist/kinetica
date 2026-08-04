---
name: Kinetica
description: Use when querying and managing GPU-accelerated databases, loading data from multiple sources, executing SQL analytics, building graphs and geospatial queries, or administering Kinetica clusters. Agents should reach for this skill when users need to work with high-performance analytics, real-time data ingestion, or complex spatial/graph operations.
metadata:
    mintlify-proj: kinetica
    version: "1.0"
---

# Kinetica Skill

## Product Summary

Kinetica is a GPU-accelerated SQL database designed for real-time analytics and high-performance queries. Agents use it to execute SQL queries, load data from diverse sources (S3, Azure, GCS, JDBC, Kafka, local files), manage schemas and tables, and perform advanced analytics including geospatial queries, graph operations, and machine learning inference. The primary interface is Kinetica Workbench (web UI) or SQL via KiSQL CLI, JDBC/ODBC drivers, or REST API endpoints. Key entry points: `/execute/sql` REST endpoint, `CREATE TABLE`/`INSERT` SQL commands, Workbench UI at the cluster's web address, and native APIs (Java, Python, C++, C#, JavaScript, Node.js).

## When to Use

Reach for this skill when:
- A user needs to execute SQL queries against a Kinetica database
- Data must be loaded from external sources (S3, Azure Blob, GCS, HDFS, Kafka, JDBC, local files)
- Creating or modifying database schemas, tables, views, or indexes
- Performing geospatial or graph-based analytics
- Administering a Kinetica cluster (adding hosts, rebalancing, backups)
- Querying via REST API, SQL, or native language APIs
- Optimizing query performance or managing resource groups
- Working with materialized views, external tables, or data sources/sinks

## Quick Reference

### Essential SQL Commands

| Task | Command |
|------|---------|
| Create schema | `CREATE SCHEMA [IF NOT EXISTS] schema_name;` |
| Create table | `CREATE TABLE schema.table_name (col1 TYPE, col2 TYPE, ...);` |
| Insert data | `INSERT INTO schema.table_name VALUES (...);` or `INSERT INTO ... SELECT ...;` |
| Load from file | `LOAD INTO schema.table_name FROM FILE 'path/to/file.csv';` |
| Query data | `SELECT * FROM schema.table_name WHERE condition;` |
| Create view | `CREATE VIEW schema.view_name AS SELECT ...;` |
| Create materialized view | `CREATE MATERIALIZED VIEW schema.mv_name AS SELECT ...;` |
| Create external table | `CREATE EXTERNAL TABLE schema.ext_table (...) AS SELECT FROM DATA SOURCE ...;` |
| Create data source | `CREATE DATA SOURCE ds_name TYPE 's3' LOCATION 'bucket/path' CREDENTIAL cred_name;` |
| Create credential | `CREATE CREDENTIAL cred_name TYPE 's3' IDENTITY 'key' SECRET 'secret';` |

### REST API Endpoints (Common)

| Endpoint | Purpose |
|----------|---------|
| `/execute/sql` | Execute SQL statements (queries, DML, DDL) |
| `/insert/records/json` | Insert records in JSON format |
| `/get/records` | Retrieve records with optional filtering |
| `/filter/*` | Filter data by range, geometry, radius, string, etc. |
| `/aggregate/*` | Aggregation operations (groupby, statistics, histogram, kmeans) |
| `/create/table` | Create a table via REST |
| `/show/table` | Show table metadata and structure |
| `/admin/show/cluster/operations` | Check cluster operation status |
| `/admin/rebalance` | Rebalance data across cluster nodes |

### Connection Strings

**REST (HTTP):** `http://<host>:9191`  
**REST (HTTPS):** `https://<host>:8082/gpudb-0`  
**JDBC:** `jdbc:kinetica:http://<host>:9191`  
**Python:** `gpudb.GPUdb(host=['http://<host>:9191'], options=options)`  
**Java:** `new GPUdb("http://<host>:9191", options)`

### Key Configuration Files

- `gpudb.conf` — Main cluster configuration (on each node)
- `gadmin.conf` — GAdmin web interface configuration
- System properties accessible via `SHOW SYSTEM PROPERTIES` or `/show/system/properties`

## Decision Guidance

### When to Use SQL vs. REST API

| Scenario | Use SQL | Use REST |
|----------|---------|----------|
| Interactive queries from CLI/Workbench | ✓ | |
| Programmatic data insertion from app | | ✓ |
| Complex joins and aggregations | ✓ | |
| Bulk record insertion | ✓ (INSERT) | ✓ (/insert/records) |
| Geospatial filtering | ✓ | ✓ (/filter/byarea, /filter/byradius) |
| Graph operations | ✓ | ✓ (/create/graph, /match/graph) |

### When to Use External Tables vs. Data Sources

| Approach | Use When |
|----------|----------|
| **External Table** | Data is in cloud storage (S3, Azure, GCS) and you want to query it directly without copying; supports lazy loading |
| **Data Source + LOAD** | You want to ingest data into Kinetica tables; supports transformation and indexing |
| **Direct INSERT** | Data is small or already in memory; fastest for known schemas |

### When to Use Materialized Views vs. Regular Views

| Type | Use When |
|------|----------|
| **Regular View** | Query is simple; storage overhead not a concern; data changes frequently |
| **Materialized View** | Query is expensive; data is queried repeatedly; data changes infrequently |

## Workflow

### Typical Task: Load Data and Query

1. **Understand the source:** Identify data location (S3, local file, JDBC, Kafka) and format (CSV, Parquet, JSON).

2. **Create schema and table:**
   ```sql
   CREATE SCHEMA IF NOT EXISTS my_schema;
   CREATE TABLE my_schema.my_table (
       id INT,
       name VARCHAR(100),
       amount FLOAT,
       created_date DATE
   );
   ```

3. **Create credential (if external source):**
   ```sql
   CREATE CREDENTIAL s3_cred TYPE 's3' 
       IDENTITY 'AWS_KEY' SECRET 'AWS_SECRET';
   ```

4. **Create data source (if external):**
   ```sql
   CREATE DATA SOURCE s3_source TYPE 's3' 
       LOCATION 's3://bucket/path' 
       CREDENTIAL s3_cred;
   ```

5. **Load data via SQL:**
   ```sql
   LOAD INTO my_schema.my_table 
   FROM FILE 's3://bucket/data.csv' 
   WITH OPTIONS (HEADER='true', DELIMITER=',');
   ```
   Or from data source:
   ```sql
   INSERT INTO my_schema.my_table 
   SELECT * FROM EXTERNAL TABLE (...) 
   AS SELECT * FROM DATA SOURCE s3_source;
   ```

6. **Verify data loaded:**
   ```sql
   SELECT COUNT(*) FROM my_schema.my_table;
   SELECT * FROM my_schema.my_table LIMIT 10;
   ```

7. **Execute analytics queries:**
   ```sql
   SELECT name, SUM(amount) as total 
   FROM my_schema.my_table 
   GROUP BY name 
   ORDER BY total DESC;
   ```

8. **Create indexes if needed:**
   ```sql
   CREATE INDEX idx_name ON my_schema.my_table (name);
   ```

## Common Gotchas

- **Schema must exist before creating tables:** Kinetica does not auto-create schemas. Always `CREATE SCHEMA` first.
- **Primary key collisions:** By default, duplicate primary keys are rejected. Use `UPDATE_ON_EXISTING_PK = TRUE` option to replace, or `IGNORE_EXISTING_PK = TRUE` to skip.
- **External tables are read-only:** You cannot INSERT into external tables; they are query-only views of remote data.
- **Credentials are required for cloud sources:** S3, Azure, GCS all require credentials; ensure they are created before data sources.
- **Data source location format matters:** S3 paths use `s3://bucket/path`, Azure uses `wasbs://container@account.blob.core.windows.net/path`.
- **TTL (time-to-live) on tables:** Intermediate result tables from queries may have TTL set; clean them up manually if needed.
- **Materialized views are not auto-refreshed:** Use `REFRESH MATERIALIZED VIEW` to update after source data changes.
- **Geospatial columns require WKT format:** Use `ST_MAKEPOINT()`, `ST_GEOMFROMTEXT()` to create geometry objects.
- **Graph operations require directed/undirected specification:** Specify `DIRECTED = true/false` when creating graphs.
- **Query plan caching:** Disable with `PLAN_CACHE = FALSE` if query parameters change frequently.

## Verification Checklist

Before submitting work:

- [ ] Schema exists and is correct: `SHOW SCHEMA schema_name;`
- [ ] Table structure matches requirements: `DESCRIBE TABLE schema.table_name;`
- [ ] Data loaded successfully: `SELECT COUNT(*) FROM schema.table_name;`
- [ ] Sample rows are correct: `SELECT * FROM schema.table_name LIMIT 5;`
- [ ] Indexes created if needed: `SHOW TABLE schema.table_name;` (check index list)
- [ ] Credentials are valid (if using external sources): `SHOW CREDENTIAL cred_name;`
- [ ] Query executes without errors: Run query and check response status
- [ ] Query performance is acceptable: Check query timing in Workbench or via `/show/system/timing`
- [ ] No orphaned temporary tables: Check for result tables with TTL expiration
- [ ] Backup created if modifying production data: `CREATE BACKUP backup_name;`

## Resources

- **Comprehensive navigation:** https://docs.kinetica.com/llms.txt
- **SQL Reference:** https://docs.kinetica.com/content/sql/index
- **REST API Reference:** https://docs.kinetica.com/content/api/rest/index
- **Data Loading Guide:** https://docs.kinetica.com/content/load_data/index
- **Administration & Cluster Management:** https://docs.kinetica.com/content/admin/index

---

> For additional documentation and navigation, see: https://docs.kinetica.com/llms.txt