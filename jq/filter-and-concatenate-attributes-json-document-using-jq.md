# Filter and concatenate a JSON document using jq

I wanted to filter the list of the cores supported by the Arduino Builder and get a nice list with core name and version.

Here a fragment from the JSON document:

```json
{
  "items": [
    {
      "boards": [
        {
          "fqbn": "arduino:mbed_rp2040:pico",
          "name": "Raspberry Pi Pico"
        }
      ],
      "id": "arduino:mbed_rp2040",
      "installed": "2.3.1",
      "name": "Arduino Mbed OS RP2040 Boards"
    },
    {
      "boards": [
        {
          "fqbn": "arduino:megaavr:uno2018",
          "name": "Arduino Uno WiFi Rev2"
        },
        {
          "fqbn": "arduino:megaavr:nona4809",
          "name": "Arduino Nano Every"
        }
      ],
      "id": "arduino:megaavr",
      "installed": "1.8.7",
      "name": "Arduino megaAVR Boards"
    },
```

For this use case I just want the `id` (the FQBN) and the `installed` (the _installed_ version):

```shell
$ curl https://builder.arduino.cc/v1/cores | jq '.items[] | (.id + " " + .installed)'
"atmel-avr-xminis:avr 0.6.0"
"emoro:avr 3.2.2"
"esp32:esp32 1.0.6"
"esp8266:esp8266 2.5.0"
"Intel:arc32 2.0.4"
"Intel:i586 1.6.7+1.0"
"Intel:i686 1.6.7+1.0"
"arduino:samd 1.8.11"
"arduino:mbed_portenta 2.3.1"
"arduino:sam 1.6.12"
"arduino:mbed_edge 2.3.1"
"arduino:mbed_nano 2.3.1"
"arduino:mbed_rp2040 2.3.1"
"arduino:megaavr 1.8.7"
"arduino:mraa 1.0.8"
"arduino:nrf52 1.0.2"
"arduino:avr 1.8.3"
"industruino:samd 1.0.1"
"littleBits:avr 1.0.0"
"Arrow:samd 2.1.0"
"Microsoft:win10 1.1.2"
```

