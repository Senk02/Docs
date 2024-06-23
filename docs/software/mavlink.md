---
template: main.html
description: ExpressLRS Bi-directional MAVLink support
---

![Software Banner](https://raw.githubusercontent.com/ExpressLRS/ExpressLRS-Hardware/master/img/software.png)

!!! warning "Warning"
    Although MAVLink has been in development for some time, and has been tested by a community of early adopters using ArduPilot crafts, MAVLink support is still a recent addition. There may be unexpected bugs; Exercise due caution.

!!! note "NOTE"
    MAVLink is only available to receivers with ESP hardware, and **NOT STM32**. Enabling MAVLink forces the use of Hybrid or 16ch/2 switch mode. Wide switch mode is not supported.

## Description

ExpressLRS now has full bi-directional [MAVLink](https://mavlink.io/en/) support, enabling native MAVLink telemetry downlink and RC control uplink. Users can now enjoy seamless integration of telemetry and RC control.


## Flashing and Configuring the MAVLink branch

1. At the top of the ExpressLRS configurator, select "GIT BRANCH"

1. Select the `master` branch, and flash it to both the RX and TX

1. Turn on both the RX and TX, and ensure they connect properly

1. In ELRS LUA script, select `Other Devices`, select your receiver, and set the `serial protocol` to MAVLink

1. Back out to the LUA scripts main menu, and select the new `Link Mode` option. Change it from `Normal` to `MAVLink`

1. Configure your usual power, packet rate, etc. Use 1:2 for telemetry ratio (it will be auto-set)

1. Wire the RX to a free UART that is suitable for TLM + RC


## Using MAVLink on ArduPilot

1. Configure the UART in ArduPilot for MAVLink 2, at `460800` baud
    - For example, if you're using UART 3, you'd set `SERIAL3_PROTOCOL=2` and `SERIAL3_BAUD=460`
2. Connect the TX module to the computer running the Ground Control Station via a USB cable

3. Select the COM port on the GCS, and connect using `460800` baud

## Using MAVLink on PX4
1. Configure the UART with SER_TEL2_BAUD to `460800 8N1` (If you are using QGroundControl for that it is under the Parameters -> Serial settings)
2. Configure MavLink with MAV_0_CONFIG to `TELEM2`
3. Configure MavLink sending rate with MAV_0_RATE to `9600 B/s`

### QGroundControl Setting
1. In the application settings go to `Common Links` and add a new connection
2. Set a name and select the serial port (for instance if you are using linux ttyUSB0) and set the baudrate to `460800`

If you are having trouble connecting to QGC it helps to close QGC and disconnect the TX module than connect first the USB and than open QGC. Also you can select `Automatically Connect on Start` if that helps.


## Using MAVLink on INAV / Betaflight

- INAV and Betaflight contain an incomplete implementation of the MAVLink protocol standard (lacking RADIO_STATUS flow control). This causes an INAV/Betaflight aircraft to saturate the bandwidth of a telemetry link using soft flow control, and renders it unusable, ergo breaking support with ExpressLRS MAVLink.


