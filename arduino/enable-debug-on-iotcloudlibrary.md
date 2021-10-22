# Enable debug on IoT Cloud Library


Visit https://github.com/arduino-libraries/ArduinoIoTCloud/ and clone the repo on your computer.

Edit the `src/AIoTC_Config.h:65` https://github.com/arduino-libraries/ArduinoIoTCloud/blob/master/src/AIoTC_Config.h#L65 and uncomment the `Debug.print()`.


```git
diff --git a/src/AIoTC_Config.h b/src/AIoTC_Config.h
index 9ceb2ac..6df348a 100644
--- a/src/AIoTC_Config.h
+++ b/src/AIoTC_Config.h
@@ -62,7 +62,7 @@
 # if defined(ARDUINO_AVR_UNO_WIFI_REV2)
 #   define DEBUG_VERBOSE(fmt, ...)
 # else
-#   define DEBUG_VERBOSE(fmt, ...) //Debug.print(DBG_VERBOSE, fmt, ## __VA_ARGS__)
+#   define DEBUG_VERBOSE(fmt, ...) Debug.print(DBG_VERBOSE, fmt, ## __VA_ARGS__)
 # endif
 #endif
``` 

Create a ZIP file with the whole library folder:
```shell
$ zip -r ArduinoIoTCloud-with-debug.zip ArduinoIoTCloud
```

You’ll end up with a 4.9M file.

Visit https://create-dev.arduino.cc/editor

Libraries > Custom 

Click on the icon and upload your custom version of the library.


Great! Starting from now, every time you build a sketch that requires the IoTCloudLibrary this custom version will be used!

Run a new “verify and upload” using an Over-the-Air device, and now you will see additional information in the Serial Monitor, like the following output:

```
ArduinoIoTCloudTCP::onOTARequest _ota_url = https://api-dev.arduino.cc/iot/ota/a0cd5030-fae0-4ede-aa4d-63d971ebfa71
***** Arduino IoT Cloud - configuration info *****
Device ID: ba38d0c7-9bcc-412f-8073-cd6e28afa41a
Thing ID: 08f67265-01be-48a1-aa50-a1d1bf9462a4
MQTT Broker: mqtts-sa.iot.oniudra.cc:8883
WiFi.status(): 0
Current WiFi Firmware: 1.4.8
Connected to "Middle Earth"
ArduinoIoTCloudTCP::handle_SyncTime internal clock configured to posix timestamp 1634916888
Connected to Arduino IoT Cloud
ArduinoIoTCloudTCP::handle_RequestLastValues [13876] last values requested
ArduinoIoTCloudTCP::handleMessage [15886] last values received

```

## Attach to the serial

```shell
$ socat -s stdio /dev/cu.usbmodem2101
```

