# Send data every 1 to 5 seconds

I am testing the input metrics on the Azure Event Hub input, and I want a steady but now flat data flow.

I want to send a variable batch of records to my event hub on Azure.

```shell
while true; do
    # Calculate a sleep interval in the 1-5 range.
    # Thanks to https://www.warp.dev/, I discovered the nice
    # `$RANDOM` variable. This variable contains random
    # numbers between 0 and 32767.
    sleep_interval=$(( RANDOM % 5 + 1))
    
    # Send a batch of records from the .ndjson file using
    # https://github.com/zmoog/eventhubs
    eh eventdata send --lines-from-text-file activitylogs.ndjson
    
    echo "Waiting $sleep_interval seconds 🍺"
    sleep $sleep_interval
done
```
