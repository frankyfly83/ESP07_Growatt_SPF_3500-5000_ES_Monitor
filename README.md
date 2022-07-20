# ESP07_Growatt_SPF_3500-5000_ES_Monitor
This project provides Platform.io code for building custom firmware for the WiFi-F module included with the Growatt SPF 3500-5000 ES off-grid inverters. It collects all available metrics through the MODBUS interface and sends them to InfluxDB, which can then be displayed in Grafana.

[Otti's project]([https://www.google.com](https://github.com/otti/Growatt_ShineWiFi-S)) provided some inspiration, however the newer generation Wifi-F module can be a challenge to interface with. Serial adaptors (Silicon Labs, FTDI and CH340) will fail to communicate with the ESP8266 when plugged directly into the TX/RX pin headers on the PCB. The SIPEX SP3232EE RS-232 transceiver on the rear of the PCB, which is also connected to the RX and TX pins of the ESP8266, must be removed or disconnected temporarily to uploaded new firmware.

Once the SP3232 chip is removed or disconnected, the ESP8266 is easy to work with. All the necessary pins (GND, TX, RX and GPIO-0) are broken out to a standard 0.1” through holes that a pin header can be soldered to. The chip can be placed in flash mode by shorting GPIO-0 to ground while it's reset.
I've included OTA components in the firmware so any future updates can be done without a serial interface. After the initial upload, the SP3232 chip should be replaced or reconnected.

The WiFi-F board seems to be quite power hungry. Powering it through the USB plug from a source slighly above 5v will ensure the onboard buck converter can provide enough current while flashing the ESP.
