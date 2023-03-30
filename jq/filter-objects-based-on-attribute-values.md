# Filter objects based on attribute values

```shell
$ tail -f elastic-agent-20230330-92.ndjson | jq -c 'select(.log.source == "aws-cloudwatch-default") | (."@timestamp" + " " + .message)'
```

