# Enable debug on IoT Cloud Library

As of today, the [ArduinoIoTCloud](https://github.com/arduino-libraries/ArduinoIoTCloud) library does not have any specific verbose logs the trace step in the Over-the-Air (OTA) update process.

I created a [fork](https://github.com/zmoog/ArduinoIoTCloud) of the library with a few additional log statements.

Visit https://github.com/zmoog/ArduinoIoTCloud, clone the repo on your computer and check out the `zmoog/more-logs-in-ota-process` branch.

## Prepare the library fork

Create a ZIP file with the whole library folder:

```shell
$ zip -r ArduinoIoTCloud-with-debug.zip ArduinoIoTCloud
```

You’ll end up with a 4.9M file.

Visit https://create.arduino.cc/editor and click on Libraries > Custom.

Click on the icon, and upload your custom version of the library.

Great! Starting from now, every time you build a sketch that requires the IoTCloudLibrary this custom version will be used!

TIP: remove this custom library after the tests, or you won't get new updates to the original library.

Run a new “verify and upload” using an Over-the-Air device, and now you will see additional information in the Serial Monitor, like the following output:

```
***** Arduino IoT Cloud - configuration info *****
Device ID: ba38d0c7-9bcc-412f-8073-cd6e28afa41a
Thing ID: 08f67265-01be-48a1-aa50-a1d1bf9462a4
MQTT Broker: mqtts-sa.iot.oniudra.cc:8883
WiFi.status(): 0
Current WiFi Firmware: 1.4.8
Connected to "Middle Earth"
ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1635149042
ArduinoIoTCloudTCP::handle_ConnectMqttBroker connecting to mqtts-sa.iot.oniudra.cc:8883 (attempt 0)
ArduinoIoTCloudTCP::handle_ConnectMqttBroker connected to mqtts-sa.iot.oniudra.cc:8883
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/e/i ...
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/e/i
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/shadow/i ...
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/shadow/i
Connected to Arduino IoT Cloud
ArduinoIoTCloudTCP::handle_RequestLastValues [12890] last values requested
ArduinoIoTCloudTCP::handleMessage [15899] last values received
ArduinoIoTCloudTCP::onOTARequest _ota_url = https://api-dev.arduino.cc/iot/ota/732ccdfb-89dd-43e2-9206-a9bbb947b984
ArduinoIoTCloudTCP::samd_onOTARequest downloading to nina: https://api-dev.arduino.cc/iot/ota/732ccdfb-89dd-43e2-9206-a
ArduinoIoTCloudTCP::samd_onOTARequest download successful
ArduinoIoTCloudTCP::samd_onOTARequest performing reset to reboot
***** Arduino IoT Cloud - configuration info *****
Device ID: ba38d0c7-9bcc-412f-8073-cd6e28afa41a
Thing ID: 08f67265-01be-48a1-aa50-a1d1bf9462a4
MQTT Broker: mqtts-sa.iot.oniudra.cc:8883
WiFi.status(): 0
Current WiFi Firmware: 1.4.8
Connected to "Middle Earth"
ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1635154511
ArduinoIoTCloudTCP::handle_ConnectMqttBroker connecting to mqtts-sa.iot.oniudra.cc:8883 (attempt 0)
ArduinoIoTCloudTCP::handle_ConnectMqttBroker connected to mqtts-sa.iot.oniudra.cc:8883
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/e/i ...
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/e/i
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/shadow/i ...
ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/shadow/i
Connected to Arduino IoT Cloud
ArduinoIoTCloudTCP::handle_RequestLastValues [14629] last values requested
ArduinoIoTCloudTCP::handleMessage [17639] last values received
```

## How to access the serial port from the terminal

Personally, during these troubleshooting sessions I use the `minicom` utility.

Get the port currently used by the board:

```shell
$ arduino-cli board list
Port                            Protocol Type              Board Name          FQBN                     Core
/dev/cu.URT0                    serial   Unknown
/dev/cu.usbmodem1101            serial   Serial Port (USB) Arduino NANO 33 IoT arduino:samd:nano_33_iot arduino:samd
```

Open minicom using the serial port `/dev/cu.usbmodem1101`:

```shell
$ minicom -D /dev/cu.usbmodem1101
```

- [Is there an OS X terminal program that can access serial ports?](https://apple.stackexchange.com/questions/32834/is-there-an-os-x-terminal-program-that-can-access-serial-ports)
