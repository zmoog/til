# Get More Logs out of the Arduino IoTCloudLibrary

As of today, the [ArduinoIoTCloud](https://github.com/arduino-libraries/ArduinoIoTCloud) library does not have any specific verbose logs, so trace complex workflows like Over-the-Air (OTA) update process can become quite challenging.

I created a humble [fork](https://github.com/zmoog/ArduinoIoTCloud) of the library, with just a very few additional log statements.

## Get the Library Fork

Visit https://github.com/zmoog/ArduinoIoTCloud and:

- select `zmoog/more-logs-in-ota-process` from the branch dropdown on the left;
- select Code > Download ZIP from the green actions dropdown on the right;

Save the ZIP file on your computer to use it as a custom library on the Cloud Editor.

## Set up your Sketch

Make sure your sketch is configured to use the most verbose log level:

```c
//Get Cloud Info/errors , 0 (only errors) up to 4
setDebugMessageLevel(4);
```

## Upload the IoTCloudLibrary as a Custom Library on the Arduino Cloud Editor

Visit https://create.arduino.cc/editor and click on Libraries > Custom.

Click on the icon, and upload your custom version of the library.

Great! Starting from now, every time you build a sketch that requires the IoTCloudLibrary this custom version will be used!

TIP: remove this custom library after the test, or you won't get new updates to the original library.

Run a new “verify and upload” using an Over-the-Air device, and now you will see additional information in the Serial Monitor, like the following output (this is a successful OTA update):

```
## Comment: board 1st boot

[2021-10-26 11:48:22] ***** Arduino IoT Cloud - configuration info *****
[2021-10-26 11:48:22] Device ID: 46854c56-8237-49a6-93d7-217be67b1951
[2021-10-26 11:48:22] Thing ID: 298a6dc2-4018-46cd-9255-6b6c6a5007a0
[2021-10-26 11:48:22] MQTT Broker: mqtts-sa.iot.arduino.cc:8883
[2021-10-26 11:48:22] WiFi.status(): 0
[2021-10-26 11:48:22] Current WiFi Firmware: 1.4.8
[2021-10-26 11:48:26] Connected to "Middle Earth"
[2021-10-26 11:48:26] ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1635241707
[2021-10-26 11:48:27] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connecting to mqtts-sa.iot.arduino.cc:8883 (attempt 0)
[2021-10-26 11:48:30] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connected to mqtts-sa.iot.arduino.cc:8883
[2021-10-26 11:48:34] Sd card not detected
[2021-10-26 11:48:34] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/e/i ...
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/e/i
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/shadow/i ...
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/shadow/i
[2021-10-26 11:48:35] Connected to Arduino IoT Cloud
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_RequestLastValues [15670] last values requested
[2021-10-26 11:48:37] ArduinoIoTCloudTCP::handleMessage [17497] last values received

## Comment: 1st boot completed, now the sketch is running.


... time passes ...


## Comment: I click on “verify and upload” and the OTA process starts

[2021-10-26 11:50:30] ArduinoIoTCloudTCP::onOTARequest _ota_url = https://api2.arduino.cc/iot/ota/38d59aee-e004-4dd7-8b79-716c4e7678dc
[2021-10-26 11:50:30] ArduinoIoTCloudTCP::samd_onOTARequest downloading to nina: https://api2.arduino.cc/iot/ota/38d59aee-e004-4dd7-8b79-716c
[2021-10-26 11:50:44] ArduinoIoTCloudTCP::samd_onOTARequest download successful
[2021-10-26 11:50:44] ArduinoIoTCloudTCP::samd_onOTARequest performing reset to reboot

## Comment: the board resets

[2021-10-26 11:51:04] ***** Arduino IoT Cloud - configuration info *****
[2021-10-26 11:51:04] Device ID: 46854c56-8237-49a6-93d7-217be67b1951
[2021-10-26 11:51:04] Thing ID: 298a6dc2-4018-46cd-9255-6b6c6a5007a0
[2021-10-26 11:51:04] MQTT Broker: mqtts-sa.iot.arduino.cc:8883
[2021-10-26 11:51:04] WiFi.status(): 0
[2021-10-26 11:51:04] Current WiFi Firmware: 1.4.8
[2021-10-26 11:51:08] Connected to "Middle Earth"
[2021-10-26 11:51:08] ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1635241868
[2021-10-26 11:51:09] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connecting to mqtts-sa.iot.arduino.cc:8883 (attempt 0)
[2021-10-26 11:51:12] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connected to mqtts-sa.iot.arduino.cc:8883
[2021-10-26 11:51:16] Sd card not detected
[2021-10-26 11:51:16] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/e/i ...
[2021-10-26 11:51:16] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/e/i
[2021-10-26 11:51:16] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/shadow/i ...
[2021-10-26 11:51:17] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/shadow/i
[2021-10-26 11:51:17] Connected to Arduino IoT Cloud
[2021-10-26 11:51:17] ArduinoIoTCloudTCP::handle_RequestLastValues [15249] last values requested
[2021-10-26 11:51:18] ArduinoIoTCloudTCP::handleMessage [16648] last values received

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
[2021-10-26 11:48:22] ***** Arduino IoT Cloud - configuration info *****
[2021-10-26 11:48:22] Device ID: 46854c56-8237-49a6-93d7-217be67b1951
[2021-10-26 11:48:22] Thing ID: 298a6dc2-4018-46cd-9255-6b6c6a5007a0
[2021-10-26 11:48:22] MQTT Broker: mqtts-sa.iot.arduino.cc:8883
[2021-10-26 11:48:22] WiFi.status(): 0
[2021-10-26 11:48:22] Current WiFi Firmware: 1.4.8
[2021-10-26 11:48:26] Connected to "Middle Earth"
[2021-10-26 11:48:26] ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1635241707
[2021-10-26 11:48:27] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connecting to mqtts-sa.iot.arduino.cc:8883 (attempt 0)
[2021-10-26 11:48:30] ArduinoIoTCloudTCP::handle_ConnectMqttBroker connected to mqtts-sa.iot.arduino.cc:8883
[2021-10-26 11:48:34] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/e/i ...
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/e/i
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribing to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/shadow/i ...
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_SubscribeMqttTopics subscribed to /a/t/298a6dc2-4018-46cd-9255-6b6c6a5007a0/shadow/i
[2021-10-26 11:48:35] Connected to Arduino IoT Cloud
[2021-10-26 11:48:35] ArduinoIoTCloudTCP::handle_RequestLastValues [15670] last values requested
[2021-10-26 11:48:37] ArduinoIoTCloudTCP::handleMessage [17497] last values received

```
