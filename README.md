# Langfuse-data-cleaner

**Langfuse-data-cleaner** is a data cleaning tool designed specifically for processing raw data generated by Langfuse. It helps in automatic removal of expired content.

## Installing from Helm Repo

```bash
helm repo add langfuse-data-cleaner https://Pudding124.github.io/langfuse-data-cleaner
helm repo update
```

```bash
# "0 2 * * *" means the job will run daily at 2:00 AM.
cronjob:
  runtime: "0 2 * * *"

nodeSelector: {}

tolerations: []

annotations: {}

# ClickHouse Section:
clickhouse:
  enable: true                # Enable ClickHouse integration.
  retention:
    days: 30                  # Data retention period: 30 days.
  host: "langfuse-clickhouse"  # Hostname of the ClickHouse server.
  port: "9000"                # Port to connect to ClickHouse.
  user: "default"             # Username for authentication.
  password: "changeme"        # Password.
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