# Filter a big JSON document using jq

I wanted to filter the list of the boards supported by the Arduino Builder to find a few ones matching a search critiera.

In this case, the search criteria was a specific board FQBN.

The Builder offers the list of the supported board using the following endpoint:

```shell
$ curl 'https://builder.arduino.cc/v3/boards' | jq
```

The response is a long list on JSON objects like the following:

```json
{
  "items": [
    {
      "architecture": "samd",
      "fqbn": "arduino:samd:mkrwifi1010",
      "href": "/v3/boards/arduino:samd:mkrwifi1010",
      "name": "Arduino MKR WiFi 1010",
      "package": "arduino",
      "plan": "create-free"
    }
  ]
}
```

I want to get only the board using the `arduino:mbed_nano:` core:

```shell
$ curl 'https://builder.arduino.cc/v3/boards' | jq '.items[] | select(.fqbn | contains("arduino:mbed_nano:"))'
{
  "architecture": "mbed_nano",
  "fqbn": "arduino:mbed_nano:nanorp2040connect",
  "href": "/v3/boards/arduino:mbed_nano:nanorp2040connect",
  "name": "Arduino Nano RP2040 Connect",
  "package": "arduino",
  "plan": "create-free"
}
{
  "architecture": "mbed_nano",
  "fqbn": "arduino:mbed_nano:nano33ble",
  "href": "/v3/boards/arduino:mbed_nano:nano33ble",
  "name": "Arduino Nano 33 BLE",
  "package": "arduino",
  "plan": "create-free"
}
```
