# Replace text with sed

Today I was collecting Azure Functions logs using the github.com/zmoog/eventhubs CLI tool.

Unfortunately, these logs from Azure are malformed due to the use of single quote instead of double quotes.

So I replaced the single quotes with the double ones to be able to use `jq`.

```shell
# Start collecting logs and store them in a .ndjson file.
eh eventdata receive > mbranca-general.functionapplogs.ndjson

# Run some commands to inspect the logs
$ cat mbranca-general.functionapplogs.ndjson | wc -l
      13
$ cat mbranca-general.functionapplogs.ndjson | sed "s/\'/\"/g" | jq '.records[].time' | wc -l
     367
```
