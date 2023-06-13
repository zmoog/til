# Add a new key to an existing object

To use jq to add a new key from an existing one, you can use the |= operator to modify an existing key or add a new key to an object. Here's an example.

Suppose you have a JSON file data.json with the following contents:

```json
{
  "id": 2987942903,
  "description": "sync",
  "start": "2023-05-30T04:25:46+00:00",
  "stop": "2023-05-30T05:05:46+00:00",
  "duration": 2400,
  "tags": [
    "type:sync"
  ]
}
```

You can use the following `jq` command to add a new key `@timestamp` to the object, which is the value of the `start` key:

```
jq '. | ."@timestamp" = .start'   
```

This will output the following JSON:

```json
{
  "id": 2987942903,
  "description": "sync",
  "start": "2023-05-30T04:25:46+00:00",
  "stop": "2023-05-30T05:05:46+00:00",
  "duration": 2400,
  "tags": [
    "type:sync"
  ],
  "@timestamp": "2023-05-30T04:25:46+00:00"
}
```
