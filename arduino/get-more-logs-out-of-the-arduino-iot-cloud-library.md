# Get More Logs out of the Arduino IoTCloudLibrary

As of today, the [ArduinoIoTCloud](https://github.com/arduino-libraries/ArduinoIoTCloud) library does not have any specific verbose logs, so trace complex workflows like Over-the-Air (OTA) update process can become quite challenging.

I created a humble [fork](https://github.com/zmoog/ArduinoIoTCloud) of the library, with just a very few additional log statements.

## Get the Library Fork

Visit https://github.com/zmoog/ArduinoIoTCloud and:

- select `zmoog/more-logs-in-ota-process` from the branch dropdown on the left;
- select Code > Download ZIP from the green actions dropdown on the right;

Save the ZIP file on your computer to use it as a custom library on the Cloud Editor.

## Upload the IoTCloudLibrary as a Custom Library on the Arduino Cloud Editor

Visit https://create.arduino.cc/editor and click on Libraries > Custom.

Click on the icon, and upload your custom version of the library.

Great! Starting from now, every time you build a sketch that requires the IoTCloudLibrary this custom version will be used!

TIP: remove this custom library after the test, or you won't get new updates to the original library.

Run a new “verify and upload” using an Over-the-Air device, and now you will see additional information in the Serial Monitor, like the following output (this is a successful OTA update):

```
## Comment: board 1st boot

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

## Comment: 1st boot completed, now the sketch is running.

... time passes ...

## Comment: I click on “verify and upload” and the OTA process starts

ArduinoIoTCloudTCP::onOTARequest _ota_url = https://api-dev.arduino.cc/iot/ota/732ccdfb-89dd-43e2-9206-a9bbb947b984
ArduinoIoTCloudTCP::samd_onOTARequest downloading to nina: https://api-dev.arduino.cc/iot/ota/732ccdfb-89dd-43e2-9206-a
ArduinoIoTCloudTCP::samd_onOTARequest download successful
ArduinoIoTCloudTCP::samd_onOTARequest performing reset to reboot

## Comment: the board resets

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

## Comment: the process completed successfully.
```

## Optional: How to access the serial port from the terminal

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

TIP: Pressing `Meta-N` on the `minicom` console you also get a nice timestamp on each line:

```
***** Arduino IoT Cloud - configuration info *****
Device ID: ba38d0c7-9bcc-412f-8073-cd6e28afa41a
[2021-10-26 10:50:59] Thing ID: 08f67265-01be-48a1-aa50-a1d1bf9462a4
[2021-10-26 10:50:59] MQTT Broker: mqtts-sa.iot.oniudra.cc:8883
[2021-10-26 10:50:59] WiFi.status(): 0
[2021-10-26 10:50:59] Current WiFi Firmware: 1.4.8
[2021-10-26 10:51:03] Connected to "Middle Earth"
[2021-10-26 10:51:04] ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1635238264
[2021-10-26 10:51:05] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connecting to mqtts-sa.iot.oniudra.cc:8883 (attempt 0)
[2021-10-26 10:51:08] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connected to mqtts-sa.iot.oniudra.cc:8883
[2021-10-26 10:51:09] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/e/i ...
[2021-10-26 10:51:09] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/e/i
[2021-10-26 10:51:09] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/shadow/i ...
[2021-10-26 10:51:09] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/08f67265-01be-48a1-aa50-a1d1bf9462a4/shadow/i
[2021-10-26 10:51:09] Connected to Arduino IoT Cloud
[2021-10-26 10:51:10] ArduinoIoTCloudTCP::handle_RequestLastValues [14079] last values requested
[2021-10-26 10:51:14] ArduinoIoTCloudTCP::handleMessage [18089] last values received

```

- [Is there an OS X terminal program that can access serial ports?](https://apple.stackexchange.com/questions/32834/is-there-an-os-x-terminal-program-that-can-access-serial-ports)
