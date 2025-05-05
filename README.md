# Langfuse-data-cleaner

**Langfuse-data-cleaner** is a tool for setup the clichouse ttl

## Installing from Helm Repo

```bash
helm repo add langfuse-data-cleaner https://Pudding124.github.io/langfuse-data-cleaner
helm repo update
```

```bash
nodeSelector: {}

tolerations: []

annotations: {}

# ClickHouse Section:
clickhouse:
  enable: true
  cluster_enabled: false         
  cluster_name: default
  ttl:
    tables:
      - name: event_log
        ttl_column: created_at
        interval: 2 DAY
  host: "langfuse-clickhouse-headless.default.svc.cluster.local"  # Hostname of the ClickHouse server.
  port: "9000"                # Port to connect to ClickHouse.
  user: "default"             # Username for authentication.
  password: "changeme"        # Password.
```
## How to find the leader of clickhouse in k8s headless
1. Connect to your clickhouse
```bash
clickhouse-client --host langfuse-clickhouse.default.svc.cluster.local --user default --password 123456
```
2. excute the sql
```sql
SELECT database, table, replica_path, replica_name, is_leader FROM system.replicas WHERE is_leader = 1;

Query id: 055eae99-ad40-4d38-9ac2-f8cf74129f1b

┌─database─┬─table────────────────┬─replica_path──────────────────────────────────────────────────────────────────────────────────────────────┬─replica_name──────────────────────┬─is_leader─┐
│ default  │ observations         │ /clickhouse/tables/7ea14183-f287-48b2-add1-3b0d72f6c0f0/shard0/replicas/mars-langfuse-clickhouse-shard0-1 │ mars-langfuse-clickhouse-shard0-1 │         1 │
│ default  │ project_environments │ /clickhouse/tables/3c46c131-71d6-42c2-8897-7f0fc44d20bc/shard0/replicas/mars-langfuse-clickhouse-shard0-1 │ mars-langfuse-clickhouse-shard0-1 │         1 │
│ default  │ schema_migrations    │ /clickhouse/tables/293efb1f-99c5-40cd-a975-514fb1f57d23/shard0/replicas/mars-langfuse-clickhouse-shard0-1 │ mars-langfuse-clickhouse-shard0-1 │         1 │
│ default  │ scores               │ /clickhouse/tables/ede107a3-4e5a-42cc-85e3-f29d49b1d265/shard0/replicas/mars-langfuse-clickhouse-shard0-1 │ mars-langfuse-clickhouse-shard0-1 │         1 │
│ default  │ traces               │ /clickhouse/tables/f257098b-f358-4c4b-b4c4-ce7226052703/shard0/replicas/mars-langfuse-clickhouse-shard0-1 │ mars-langfuse-clickhouse-shard0-1 │         1 │
└──────────┴──────────────────────┴───────────────────────────────────────────────────────────────────────────────────────────────────────────┴───────────────────────────────────┴───────────┘
```


## Contributing
 
1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## License
 
The MIT License (MIT)

Copyright (c) 2015 Chris Kibble

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.