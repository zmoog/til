# VerneMQ Webhooks

Today I was looking at a quick way to test a new `on_deliver` hook on our development VerneMQ cluster and, thanks to a kind suggestion from a team mate, I finally noted the nice webhooks-related commands from the VerneMQ CLI.

## List existing webhooks

```shell
$ vmq-admin webhooks show
+-------------------+--------------------------------------------+---------------+------------------+
| hook              | endpoint                                   | base64payload | response_timeout |
+-------------------+--------------------------------------------+---------------+------------------+
| on_publish        | http://127.0.0.1:8000/v1/on_publish        | true          | 5000             |
+-------------------+--------------------------------------------+---------------+------------------+
```

## Register a new hook

```shell
$ vmq-admin webhooks register hook=on_deliver endpoint="http://127.0.0.1:8000/v1/on_deliver"
Done
```

## Deregister a exising hook

```shell
$ vmq-admin webhooks deregister hook=on_deliver endpoint="http://127.0.0.1:8000/v1/on_deliver"
Done
```
