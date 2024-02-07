## Best queries to find tables that needed indexes

```sql
SELECT schemaname, relname, seq_scan, seq_tup_read,
       seq_tup_read / seq_scan AS avg, idx_scan
FROM pg_stat_user_tables
WHERE seq_scan > 0
ORDER BY seq_tup_read DESC LIMIT 2
```

```sql
SELECT schemaname, relname, indexrelname, idx_scan,
       pg_size_pretty(pg_relation_size(indexrelid))
AS idx_size,
       pg_size_pretty(sum(pg_relation_size(indexrelid))
               OVER (ORDER BY idx_scan, indexrelid))
AS total
FROM   pg_stat_user_indexes
ORDER BY 6;
```

## Best query to find which queries are too slow in the system. But before execute, need to follow these steps:

1. Add `pg_stat_statements` to `shared_preload_libraries` in the `postgresql.conf` file.
2. Restart the database server.
3. Run `CREATE EXTENSION pg_stat_statements` in the databases of your choice.

```sql

SELECT  round((100 * total_exec_time /
sum(total_exec_time)
                OVER ())::numeric, 2) percent,
        round(total_exec_time::numeric, 2) AS total,
        calls,
        round(mean_exec_time::numeric, 2) AS mean,
        substring(query, 1, 40)
FROM    pg_stat_statements
ORDER BY total_exec_time DESC
LIMIT 10;
```

