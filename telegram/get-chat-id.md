# Get a chat id

Let's say you are working on a simple Telegram client, and you want to get the chat id of a user or a group to send test messages.

According to https://stackoverflow.com/questions/32423837/telegram-bot-how-to-get-a-group-chat-id, here's the quickest way to get a user or group chat id is:

```shell
$ curl -i -XGET "https://api.telegram.org/TOKEN/getUpdates"
HTTP/2 200 
server: nginx/1.18.0
date: Thu, 09 Feb 2023 05:18:02 GMT
content-type: application/json
content-length: 336
strict-transport-security: max-age=31536000; includeSubDomains; preload
access-control-allow-origin: *
access-control-allow-methods: GET, POST, OPTIONS
access-control-expose-headers: Content-Length,Content-Type,Date,Server,Connection
{
  "ok": true,
  "result": [
    {
      "update_id": 123,
      "message": {
        "message_id": 123,
        "from": {
          "id": 123,
          "is_bot": false,
          "first_name": "Maurizio",
          "last_name": "Branca",
          "username": "zmoog",
          "language_code": "en"
        },
        "chat": {
          "id": 161035319,
          "first_name": "Maurizio",
          "last_name": "Branca",
          "username": "zmoog",
          "type": "private"
        },
        "date": 1675919879,
        "text": "hey"
      }
    }
  ]
}
```
