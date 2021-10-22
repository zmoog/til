# How to dump MQTT messages using mosquitto_sub

As a developer, I want to dump all the messages published in a set of MQTT topics in the terminal.

I need a few parameters:

 - `USERNAME`: username
 - `PASSWORD`: password
 - `THING_ID`: `b89e2d30-1d3a-4e4f-a3f5-212250a9cf23`
 - `CLIENT_ID`: `a:app:$USERNAME:1`


```shell
$ mosquitto_sub -L mqtts://$USERNAME:$PASSWORD@$MQTT_BROKER:$MQTT_PORT//a/t/$THING_ID/+/+ -i $CLIENT_ID -v --tls-version tlsv1.2 -d --insecure -q 0 -d -F %X

Client a:app:username:1 sending CONNECT
Client a:app:username:1 received CONNACK (0)
Client a:app:username:1 sending SUBSCRIBE (Mid: 1, Topic: /a/t/b89e2d30-1d3a-4e4f-a3f5-212250a9cf23/+/+, QoS: 0, Options: 0x00)
Client a:app:username:1 received SUBACK
Subscribed (mid: 1): 0
Client a:app:username:1 received PUBLISH (d0, q0, r0, m0, '/a/t/b89e2d30-1d3a-4e4f-a3f5-212250a9cf23/e/o', ... (15 bytes))
9FA20066757074696D650219DCEAFF

```

