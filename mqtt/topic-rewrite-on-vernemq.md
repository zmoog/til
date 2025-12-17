# Topic rewrite on VerneMQ

I want the MQTT client to subscribe to VerneMQ using a device ID based topic name, but to actually subscribe to a different topic.

For example, I want the MQTT client to being able to subscribe a topic named `/device/123` so it must only know its device ID (`123` in this example).

Since the device can chage over time I want the data to be published to the topic `/thing/456`.

VerneMQ has a nice feature called topic rewrite, available for both `SUBSCRIBE` and `PUBLISH` contro packets from the MQTT protocol.

The subscribe can be customized using the [auth_on_subscribe](https://docs.vernemq.com/plugindevelopment/subscribeflow#auth_on_subscribe-and-auth_on_subscribe_m5) hook.

The publish can be customized using the [auth_on_publish](https://docs.vernemq.com/v/master/plugin-development/publishflow#auth_on_publish-and-auth_on_publish_m5) hook.


```
┌──────────┐                   ┌─────────────┐         ┌─────────────┐
│  client  │                   │ mqtt broker │         │   plugin    │
└──────────┘                   └─────────────┘         └─────────────┘
      │                               │                       │
      │                               │                       │
      │          subscribe            │                       │
      │         /device/123           │                       │
      │  ──────────────────────────▶  │                       │
      │                               │      auth_on_su       │
      │                               │ ──────bscribe───────▶ │
      │                               │                       │
      │                               │     rewrite w/        │
      │                               │ ◀ ─ /thing/456─ ─ ─ ─ │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
      │                               │                       │
                                      │                       │
```