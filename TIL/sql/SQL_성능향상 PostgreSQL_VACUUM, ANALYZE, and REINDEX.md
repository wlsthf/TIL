# SQL_성능향상 PostgreSQL_VACUUM, ANALYZE, and REINDEX



```sql
select name, setting from pg_settings where name = 'autovacuum' ;
```



## 1. Vacuum

```sql
-- 	Plain VACUUM: Frees up space for re-use
VACUUM [tablename]

-- Full VACUUM: Locks the database table, and reclaims more space than a plain VACUUM
/* Before Postgres 9.0: */
VACUUM FULL
/* Postgres 9.0+: */
VACUUM(FULL) [tablename]

-- Full VACUUM and ANALYZE: Performs a Full VACUUM and gathers new statistics on query executions paths using ANALYZE
/* Before Postgres 9.0: */
VACUUM FULL ANALYZE [tablename]
/* Postgres 9.0+: */
VACUUM(FULL, ANALYZE) [tablename]

-- Verbose Full VACUUM and ANALYZE: Same as #3, but with verbose progress output
/* Before Postgres 9.0: */
VACUUM FULL VERBOSE ANALYZE [tablename]
/* Postgres 9.0+: */
VACUUM(FULL, ANALYZE, VERBOSE) [tablename]
```





## 2. ANALYZE

```sql
ANALYZE VERBOSE [tablename]
```





## 3. REINDEX

```sql
-- Recreate a single index, myindex:
REINDEX INDEX myindex

-- Recreate all indices in a table, mytable:
REINDEX TABLE mytable

-- Recreate all indices in schema public:
REINDEX SCHEMA public

-- Recreate all indices in database postgres:
REINDEX DATABASE postgres

-- Recreate all indices on system catalogs in database postgres:
REINDEX SYSTEM postgres
```