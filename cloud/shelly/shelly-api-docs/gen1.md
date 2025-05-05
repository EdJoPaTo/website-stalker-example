Shelly Family Overview
==========

These pages describe the HTTP API exposed by the Shelly family of devices.

Devices in the Shelly family are IoT nodes connected to the Internet over WiFi. All devices support a common set of configuration parameters, some share common features. Apart from these, each device extends the common HTTP endpoints with a set of device-specific settings and behavior.

WiFi Modes
----------

Shelly devices can operate as either WiFi Access Point (AP mode) or Client Mode (STA). The factory default is AP mode with SSID `shelly<MODEL>-XXXXXXXXXXXX` with no authentication enabled.

Initially, devices come preprogrammed in Access Point mode with no password set. To be able to connect to Allterco's cloud service, synchronize time, etc. the device has to be configured to connect to an existing, Internet-connected WiFi infrastructure.

Connecting the device to an existing WiFi infrastructure can be done:

* Via Allterco's mobile applications for Android and iOS
* Using the local web interface via a browser (open http://192.168.33.1/ )
* By performing a HTTP request to set the desired WiFi settings (see HTTP API below).

Control of these parameters via HTTP is possible via the [`/settings/sta`](#settings-sta) and [`/settings/ap`](#settings-ap) endpoints.

HTTP Server
----------

All devices run a local HTTP server on port 80. It serves as a simple web page which allows the user to setup basic parameters. While in AP WiFi mode, the web page can be accessed at:

<http://192.168.33.1/>

The web interface makes use of the HTTP endpoints described in this document. HTTP authentication is disabled by default.

mDNS Discovery
----------

Shelly devices announce a HTTP service on port 80 via mDNS. Hostname is always in the form of `shelly<model>-XXXXXXXXXXXX`.

SNTP Time Sync
----------

Shelly devices do not have a built-in real time clock but will automatically synchronize their clock when in WiFi Client mode and there is connection to the Internet. Once the time is synchronized devices can execute commands triggered by user-defined weekly schedule or based on sunrise and sunset times. Geolocation data used for sun events is obtained automatically from the public IP address of the device. However, if this fails, `tzautodetect` can be disabled and the timezone and geolocation data (for sunrise and sunset calculation) can be set manually. The default NTP server is `time.google.com`, but a custom one can also be configured.

Local actions
----------

Since v1.7.0 Shelly devices support "local" action URLs. This allows devices to invoke actions not only on other devices, but on themselves as well. To execute a local action, the action URL should be set with a prefix `http://localhost/`.

For example, to make relay 1 turn on when relay 0 is turned on:

`deviceIP/settings/relay/0?out_on_url=http://localhost/relay/1?turn=on`

Cloud
----------

Shelly devices can report their settings and state to an Internet connected cloud service. The cloud service can modify the settings and change the device state. All communication is over SSL. This service allows device monitoring and control over the Internet using the accompanying mobile applications.

CoIoT
----------

Shelly devices implement a CoAP-based protocol for monitoring which we call [CoIoT](#coiot-protocol).

Based on Mongoose-OS
----------

Shelly devices are built on top of, and along with [Mongoose-OS](https://mongoose-os.com/). Mongoose provides an integrated framework for secure sockets, over-the-air updates, application storage, common device housekeeping tasks and more, that are making the reliability and security of the Shelly portfolio possible.

Feedback
----------

If you find issues with this documentation or have other questions or comments about Shelly devices, please email [developers@shelly.cloud](mailto:developers@shelly.cloud)

Changelog
----------

Revision
Date
Description
v1.14.0
09.08.2023
* [All devices] Add option to enable/disable the ability to reset devices to AP mode by quick successive power-on events. It can be enabled from local web UI from Settings, or by endpoint /settings?pon\_wifi\_reset=true. A delay from 1 second is needed before doing the power cycle. For lights, one should wait at least 5 seconds before power cycle.
v1.13.0
02.05.2023
* [All devices] Fix ECO mode proper enabling/disabling
* [All devices] Fix showing 0 degrees as device temperature after reboot
* [All devices] Fix device and channel name with special characters
* [All devices] Fix sunset/sunrise schedules on DST day
* [All devices] Network improvements on OS level which fix most of devices disconnections
* [All devices] Fix cloud issue which prevents devices to reconnect to the cloud until reboot is applied
* [MQTT ] Fix closing connection properly on disconnect, which causes issues with publishing announce and online topics after power cycle
* [Shelly RGBW2] Fix activation switch button mode to reset timer only on off state
* [Shelly Dimmer 1/2] Fix WiFi settings not cleared after factory reset
* [Shelly Button1] Fix executing more than 1 action
* [Battery devices] Improve actions execution logic to be more responsive
* [Shelly 1/1PM with addon] Fix MQTT not publishing all topics
* [Shelly Duo RGBW] Fix turning off the light from auto off timer when there is effect enabled
* [Shelly Duo] Fix unintentional brightness change when toggling fast light from the app
* [Shelly 1PM] Prevent issue with power calculation on different production batches
* [Shelly 3EM] Fix calibration from one channel to another and calibration with N clamp
* [Shelly Dimmer 1/2] Fix dim command IP/light/0?dim=up&step=X (or dim=down)
* [Shelly RGBW2-white] Fix power on default mode working only for first channel
* [Shelly RGBW2, Duo RGBW] Fix power consumption events when dynamically changing the brightness
v1.12.1
31.10.2022
* [Shelly Door/Window 2] Fix issue with false wake-ups from the lux sensor
* [Shelly Door/Window 2] Fix false vibration alarms
* [Shelly Dimmer 2] Release stable firmware which addresses flickering issues
* [Shelly Dimmer 1] Fix dimming with buttons.
* [Shelly i3] Fix random false inputs
* [Shelly HT, Flood, Door/Window 2] Fix setting URL actions in Fahrenheit for more than 60 degrees in local web interface
* [Shelly HT, Flood, Door/Window 1/2, Button1] Error handling - In case of error, the device will report null as value on its sensor attributes, instead of 0 as in the previous FW version. Validity of the status packet can be checked by the two attributes:is\_valid: true/false - it indicates of the device have a valid status received from STM chip. sensor\_eror: number - If it is different than 0, it indicates that there was an error with its peripherals. A valid status packet is that with is\_valid: true and sensor\_error: 0
v1.12.0
09.08.2022
* [All devices] Fix issue that prevents some actions from execution
* [All devices] Nightmode is added as a channel specific object in settings json
* [All relay devices] Fix source of last command for button press
* [Shelly Flood] Fix rain mode operation
* [Shelly Duo RGBW] Fix issue that flips brightness and temp after FW upgrade
* [Shelly EM] Display correct PF in local web interface
* [Shelly i3] Fix unresponsive inputs
* [Shelly Button, Shelly i3] Fix sending empty MQTT message after long press
* [Shelly i3] Add last input sequence to status packet
* [Shelly RGBW2-white] Add nightmode support
* [Shelly 2.5] Added ends\_delay setting
* [Shelly 1PM, Shelly 1L] Fix input state after reboot
* [Shelly Duo] Add setting to choose device submodel
* [Shelly Dimmer 1/2] Add dim and step parameters for dimming with exact percentage
* [Shelly 3EM] Fix issue where PF always is diplayed as 1
* [Shelly 3EM] Add setting for consumption indicator
* [Shelly 3EM] Add support for range extender which will allow measuring more than 70A
* [Shelly 3EM] Add support for measuring on Neutral clamp. Calibration is needed.
* [Shelly 3EM] Add option to calibrate single transformer
* [Shelly 3EM] Fix bug that doesn't allow storing more than 24kWh in internal flash
v1.11.0
15.07.2021
* [All devices] Fix disconnection issues
* [All devices] Fix ghost relay switches
* [All devices] Fix bug with changing DNS
* [All devices] Fix bug with keeping old static wifi config after new wifi settings
* [All devices] Fix MQTT queue overflow
* [All devices] Fix MQTT periodic updates
* [All devices] Fix bug with not applying the new wifi configuration immediately
* [Shelly Dimmer 1/2, Shelly Bulb RGBW, Shelly Duo, Shelly Vintage, Shelly RGBW2 white/color] Add one-shot transition parameter in light/0/set MQTT command and /light/0 HTTP endpoint
* [Shelly Dimmer 2] Fix flickering while the input is on
* [Shelly H&T] Add sensor/ext\_power MQTT topic to indicate if the device is USB powered. Also, the device will show 100% battery level if on USB power
* [Shelly 2, Shelly 2.5] Add mode attribute to the MQTT announce topic
* [Shelly Door/Window 1/2, Shelly Flood] Deprecated API Remove HTTP parameter /settings?sleep\_mode\_period
* [Shelly Door/Window 1/2] Add dwStateChanged attribute to CoAP packet that indicates if the door/window state is changed with the current status. The short status on opening/closing the door/window is deprecated. Instead, a normal status is sent on every event.
* [Shelly Door/Window 1/2, Shelly H&T, Shelly Flood, Shelly Button1] Add fast connect to significantly decrease connect time on wakeup
* [Shelly Uni] ADC value is updated on 0.01V change, instead of 0.5V
* [Shelly Bulb RGBW] Fix transition on power-on
* [Shelly Bulb RGBW] Fix auto-off timer on power-on
* [Shelly Bulb RGBW] Fix dimming to 0% brightness after weekly schedule turn off
* [Shelly Bulb RGBW] Show only attributes for the current mode (color/white) in the CoAP and HTTP status packet
* [Shelly Bulb RGBW] Add endpoint device\_submodel for choosing E27 or GU10 submodel. This is used in the calculation of the power consumption
* [Shelly Bulb] Fix broken CoAP packet
* [Shelly 1L] Fix recording consumption data in the mobile app when the relay is off
* [Shelly 2.5] Fix not erasing data on factory reset when in roller mode
* [Shelly 2, Shelly 2.5] Add mode attribute to the MQTT announce topic
* [Shelly Button1] Fix broken CoAP packet
* [Shelly EM, Shelly 3EM] Fix issue with not reporting valid timezone
* [Shelly 3EM] Add total\_power attribute in the status json, which is sum of the power of the three channels
* [Shelly 3EM] Remove min V and max V from the example of the .csv file in the documentation
* [Shelly RGBW2 white/color] Rework transitions to be smoother
* [Shelly RGBW2 white/color] Fix weekly schedules not working when set to 0% brightness
v1.10.0
02.03.2021
* [All devices] Add new property fanSpeed to CoIoT
* [All devices] Add new unit pct to CoIoT
* [All devices] Add new endpoint /cit/d to retrieve CoIoT description package over HTTP
* [All devices] Add attributes ap\_roaming.enabled, ap\_roaming.threshold and parameters ap\_roaming\_enabled, ap\_roaming\_threshold to /settings endpoint
* [All devices] Add attributes coiot.enabled, coiot.peer and parameters coiot\_enable, coiot\_peer to /settings endpoint
* [All devices] Add attribute/parameter debug\_enable to /settings endpoint
* [All devices] Add attribute/parameter allow\_cross\_origin to /settings endpoint
* [All devices] Fix unixtime to be UTC
* [All devices] Add new endpoint /ota/check
* [All devices] Add new endpoints /debug/log and /debug/log1
* [All devices] Add mode to MQTT shellies/\<shellymodel\>-\<deviceid\>/announce response (when applicable)
* [All devices] Update description of /settings/actions endpoint
* [All devices] Make it possible to retain MQTT LWT topic (add attribute mqtt.retain and parameter mqtt\_retain to /settings endpoint)
* [All devices] Add info on max supported schedule rules
* [Shelly Door/Window 1/2, Shelly H&T, Shelly Smoke, Shelly Flood, Shelly Button1] Add new endpoint /sta\_cache\_reset
* [Shelly 1/1PM, Shelly 2, Shelly 2.5, Shelly Plug/PlugS, Shelly EM, Shelly 3EM] Add attribute/parameter wifirecovery\_reboot\_enabled to /settings endpoint
* [Shelly 1/1PM/1L, Shelly 2, Shelly 2.5, Shelly I3, Shelly Uni, Shelly Dimmer 1/2, Shelly RGBW2] Clear input events after a pre-defined lifetime; don't publish input events on periodic MQTT updates
* [Shelly 1PM, Shelly 2.5, Shelly I3] Add MQTT topic shellies/\<model\>-\<deviceid\>/temperature\_status
* [Shelly 1L] Update possible values of attribute/parameter default\_state in /settings endpoint
* [Shelly 2.5] Drop meters array from /settings endpoint
* [Shelly Dimmer 2] Add attributes/parameters pulse\_mode\_detected, pulse\_mode\_rebooted, load\_autodetect to /settings endpoint
* [Shelly Dimmer 2] Add attributes calibrated, calib\_status, calib\_running, wire\_mode and forced\_neutral to /status endpoint
* [Shelly Dimmer 1/2] Add attribute/parameter zcross\_debounce to /settings endpoint
* [Shelly Dimmer 1/2] Change type of attribute loaderror (from bool to number) in /status endpoint
* [Shelly Door/Window 1/2] Add report\_url (URL to report sensor events on) to /settings/actions endpoint
* [Shelly Door/Window 1/2] Add attributes/parameters vibration\_sensitivity and lux\_wakeup\_enable to /settings endpoint
* [Shelly Door/Window 1/2] Update possible values of attribute act\_reasons in /status endpoint
* [Shelly Door/Window 2] Add tmp object (temperature sensor reading) to /status endpoint
* [Shelly Door/Window 2] Add temperature\_threshold, temperature\_units and temperature\_offset parameters to /settings endpoint
* [Shelly Door/Window 2] Add MQTT topic shellies/shellydw2-\<deviceid\>/sensor/temperature
* [Shelly Flood, Shelly H&T] Add id to report\_url
* [Shelly Flood] Fix sleep\_mode.period description (it's not a configurable parameter)
* [Shelly Gas] Add valves array to /status endpoint; add new endpoint /settings/valve/0
* [Shelly Gas] Add MQTT topics shellies/shellygas-\<deviceid\>/valve/0/state and shellies/shellygas-\<deviceid\>/valve/0/command
* [Shelly Bulb] Fix description of effects
* [Shelly Uni] Add missing input events to /status endpoint
* [Shelly Button1] Store input attribute event\_cnt to RTC memory when device goes to sleep
v1.9.0
24.11.2020
* [All devices] Wi-Fi re-connection issue which cause short network outage is fixed
* [All devices] Limit device and channel name up to 30 characters
* [All devices] Auto On/Off logic fixes
* [All devices] Wi-Fi re-connection issue which cause short network outage is fixed
* [All devices] Few minor or internal firmware issue are fixed
* [Shelly Dimmer/SL, Bulb, Vintage, Duo, RGBW2-color/white] Add new attribute source to /status endpoint
* [Shelly 1PM, Shelly 2.5, Shelly i3] Add temperature\_status attribute to /status payload
* [Shelly Dimmer/SL] Add attribute overpower to meters /status payload, which is value in Watts, on which an overpower condition is detected
* [Shelly Dimmer/SL] Publish new MQTT topic shellies/shellydimmer-\<deviceid\>/light/0/overpower\_value, which reports the value in Watts, on which an overpower condition is detected
* [Shelly Dimmer/SL] Add /bypass parameter to /settings endpoint
* [Shelly 2.5] Add /settings/favorites/i endpoint for setting up to 4 favorite positions in roller mode and favorites\_enabled parameter under /settings endpoint
* [Relay devices] Add appliance\_type attribute and parameter under the relay settings
* [Shelly 1PM] Add new parameter supply\_voltage to /settings endpoint
* [Shelly RGBW2-color] Add coiot\_execute\_enable parameter to /settings endpoint
* [Shelly RGBW2-color] Add transition parameter to /settings/color/X endpoint
* [Shelly RGBW2-white] Add transition parameter to /settings/white/X endpoint
* [Shelly 1/1PM] Add support for low-power switch add-on
* [Shelly 1/1PM] Allow setting of temperature and humidity offsets for temperature add-on via offset\_tC, offset\_tF parameters under /settings/ext\_temperature/{i} endpoint and offset parameter under /settings/ext\_temperature/{i} endpoint
* [Shelly 3EM] Add over\_power\_url and over\_power\_url actions for the sum of the three channels
* [Shelly H&T] Add over\_temp\_url, under\_temp\_url, over\_hum\_url and under\_hum\_url actions
* [Shelly Flood, Door/Window2] Add over\_temp\_url and under\_temp\_url actions
* [Shelly Dimmer/SL] Warm-up max time is increased to 1000 ms and logic is improved
* [Shelly Door/Window2] Battery consumption significantly improved. Some bug fixed witch cause high standby consumption
* [Shelly Plug/S] False overpower triggering and value is fixed
* [Shelly Dimmer/SL] Rotary switch support is removed by safety reasons – there is no safe rotary switch which can work on 110V-220V
* [Shelly Flood] Broken request on report\_url is fixed
* [Shelly RGBW2] Fixed crashing on specific http requests
v1.8.0
12.8.2020
* [All devices] Add key model to announce MQTT packet
* [All devices] Support multiple actions per event
* [All devices] Fix disconnection problems
* [All devices] CoAP protocol is rewritten from scratch
* [All devices] Overconsumption value can be checked in the application and the web UI
* [All devices] Devices can be updated with BETA firmware when available and can be switched to the last stable version anytime
* [All devices] Channel and device names in internal WebUI is synchronized with names from the app
* [All devices] Publish new MQTT topic shellies/\<model\>-\<deviceid\>/info on calling announce command
* [All devices] Devices can connect to open WiFi networks now
* [All devices] Fix power consumption calculation when there is no time synchronization
* [All devices] Fix bug with setting static IP
* [All devices] Local actions work with restricted device login
* [Shelly HT, Shelly Flood, Shelly Smoke] Fix battery percentage measurement
* [Shelly HT, Shelly Flood, Shelly Smoke] Fix fast battery drain on a weak WiFi coverage
* [Shelly Flood] Add temperature offset
* [Shelly Door/Window] Add parameter lux\_wakeup\_enable to /settings endpoint
* [Shelly Dimmer/SL] Add new parameter dim to /light endpoint
* [Shelly Dimmer/SL] Add new MQTT command dim
* [Shelly Dimmer/SL] Many improvements are made regarding compatibility with different dimmable loads
* [Shelly Dimmer/SL, Shelly EM, Shelly 3EM, Shelly i3, Shelly 1PM, Shelly 2.5, Shelly RGBW-color/white] Add new parameter led\_status\_disable to /settings endpoint
* [Shelly Bulb, Shelluy Duo] Fix local web page errors
* [Shelly 2.5] Fix one button mode
* [Shelly 2.5] Fix sending power updates too frequently over MQTT
* [Shelly EM, Shelly 3EM, Shelly Plug/S, Shelly 1, Shelly 1PM, Shelly 2, Shelly 2.5] Add new attribute source to /status endpoint
* [Shelly1, Shelly1PM] If add-on attached (DS1820/DHT22) Change temperature threshold on which the temperature is reported to 0.1 deg
* [Shelly RGBW2-color/white, Shelly Bulb, Shelly Vintage, Shelly Duo] Fix auto-off timer to not restart on color change
* [Shelly EM, Shelly 3EM] Fix bug with storing energy data and sending it to the cloud. Attention: All data stored in the device will be deleted, while data stored in the cloud will be not affected.
* [Shelly Gas] Add support for controlling a wired valve for liquid or gas pipes with a new endpoint /valve
* [Shelly Gas] Add new MQTT topic shellies/shellygas-XXX/valve/0/state and new MQTT command shellies/shellygas-XXX/valve/0/command
v1.7.0
26.5.2020
* [New devices] Add new devices Shelly RGBW2 Color / Shelly Shelly RGBW2 White (split from former Shelly RGBW2), Shelly Gas, Shelly i3 and Shelly Button1
* [All devices] Add attribute fw\_mode to /settings endpoint (only applicable for devices with changeable firmware mode)
* [All devices] Add attribute ram\_lwm to /status endpoint
* [All devices] Remove attribute password from /settings/login endpoint
* [All devices] Add support for local action URLs via prefix http://localhost/
* [All devices] Fix empty user agent string when calling action URLs
* [All devices] Make gateway optional when setting static IP via /settings/sta endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5, Shelly Plug, Shelly PlugS, Shelly EM, Shelly 3EM] Add attributes timer\_started and timer\_duration to /relay/{index} endpoint
* [Shelly Bulb, Shelly Vintage, Shelly Duo, Shelly Dimmer/SL] Add attributes timer\_started and timer\_duration to /light/0 endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5, Shelly Dimmer/SL] Add attributes event and event\_cnt to inputs.{index} in /status endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5, Shelly Dimmer/SL] Publish new MQTT topic shellies/\<model\>-\<deviceid\>/input\_event/\<i\>
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5] Invoke shortpush\_url and longpush\_url only if button is configured as momentary, momentary\_on\_release or detached
* [Shelly Vintage, Shelly Duo] Add parameter timer to /light/0 endpoint
* [Shelly Dimmer/SL] Add new endpoint /settings/warm\_up
* [Shelly Smoke] Add attribute/parameter temperature\_offset to /settings endpoint
* [Shelly1, Shelly1PM] Convert ext\_temperature and ext\_humidity in /settings endpoint from arrays to objects
* [Shelly1, Shelly1PM] Add attribute hwID to ext\_temperature.{index} and ext\_humidity.{index} in /status endpoint
* [Shelly1, Shelly1PM] Publish new MQTT topics shellies/\<model\>-\<deviceid\>/ext\_temperatures, shellies/\<model\>-\<deviceid\>/ext\_temperatures\_f and shellies/\<model\>-\<deviceid\>/ext\_humidities
* [Shelly Door/Window] Remove parameter closed from /calibrate endpoint, parameter opened now handles requests for both opened and closed position calibrations
* [Shelly Door/Window] Add parameter clear to /calibrate endpoint
* [Shelly Door/Window] Add attributes/parameters close\_url and vibration\_url to /settings endpoint
* [Shelly Door/Window] Change type of attribute accel.vibration in /status endpoint from bool to number, add new value -1
* [Shelly Door/Window] Add attribute accel.vibration\_time to /status endpoint
* [Shelly EM, Shelly 3EM] Remove attribute/parameter max\_power from /settings endpoint
* [Shelly EM, Shelly 3EM] Remove attribute/parameter max\_power from /settings/relay/0 endpoint
* [Shelly EM, Shelly 3EM] Add attributes/parameters over\_power\_url, over\_power\_url\_threshold, under\_power\_url, under\_power\_url\_threshold and max\_power to /settings/emeter/{index} endpoint
* [Shelly EM, Shelly 3EM] Add parameter reset\_totals to /emeter/{index} endpoint
* [Shelly EM, Shelly 3EM] Add new endpoint /reset\_data
* [Shelly EM, Shelly 3EM] Subscribe to new MQTT topic shellies/\<model\>-\<deviceid\>/emeter/\<i\>/command with message reset\_totals
* [Shelly EM, Shelly 3EM] Subscribe to MQTT topic shellies/\<model\>-\<deviceid\>/command with message reset\_data
* [Shelly 3EM] Remove attribute/parameter ctraf\_type from /settings/emeter/{index} endpoint
v1.6.0
5.3.2020
* [New devices] Add new devices Shelly Vintage, Shelly Duo, Shelly Door/Window, Shelly 3EM
* [All devices] Add attribute longid to /shelly endpoint
* [All devices] Add attribute coiot.update\_period and parameter coiot\_update\_period to /settings endpoint
* [All devices] Add attribute sntp.enabled to /settings endpoint
* [All devices] Add attributes/parameters tz\_utc\_offset, tz\_dst and tz\_dst\_auto to /settings endpoint
* [All devices] Add attribute unixtime to /status and /settings endpoints
* [All devices] Add attribute/parameter discoverable to /settings endpoint
* [All devices] Introduce per-device MQTT announce topic shellies/\<shellymodel\>-\<deviceid\>/announce
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5, Shelly RGBW2, Shelly Dimmer] Add attribute/parameter factory\_reset\_from\_switch to /settings endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5, Shelly4Pro, Shelly EM, Shelly Plug, Shelly PlugS] Add attribute timer\_remaining to /relay/{index} endpoint
* [Shelly Bulb] Add experimental attribute timer\_remaining to /light/{index} endpoint
* [Shelly Dimmer/SL] Add attribute has\_timer and experimental attribute timer\_remaining to /light/0 endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5] Add attribute/parameter longpush\_time to /settings endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5] Add new value momentary\_on\_release for attribute/parameter btn\_type in settings/relay/{index} endpoint
* [Shelly2, Shelly2.5] Hide relays or rollers arrays of hashes from /status endpoint depending on current device mode
* [Shelly2, Shelly2.5] Add attribute array inputs to /status endpoint
* [Shelly1, Shelly1PM] If add-on attached (DS1820/DHT22) Add attribute ext\_sensors.temperature\_unit to /status and /settings endpoints; add parameter ext\_sensors\_temperature\_unit to /settings endpoint
* [Shelly1, Shelly1PM] If add-on attached (DS1820/DHT22) Add attribute hash ext\_temperature and ext\_humidity to /status endpoint, add same as array of hashes to /settings endpoints
* [Shelly1, Shelly1PM] If add-on attached (DS1820/DHT22) Add new endpoints /settings/ext\_temperature/{index} and /settings/ext\_humidity/0 to configure external temperature/humidity thresholds and actions
* [Shelly1, Shelly1PM] If add-on attached (DS1820/DHT22) Publish new MQTT topics shellies/\<shellymodel\>-\<deviceid\>/ext\_temperature/\<i\>, shellies/\<shellymodel\>-\<deviceid\>/ext\_temperature\_f/\<i\> and shellies/\<shellymodel\>-\<deviceid\>/ext\_humidity/0
* [Shelly1PM] Add atrribute/parameter power\_correction to /settings endpoint
* [Shelly2] Remove voltage and current from power measurement info
* [Shelly2.5] Add attributes temperature, overtemperature and tmp attributes to /status endpoint
* [Shelly RGBW2] Add value toggle for parameter turn in subscribed MQTT topic shellies/shellyrgbw2-\<deviceid\>/white/\<n\>/set
* [Shelly Dimmer/SL] Add new value action for attribute/parameter btn\_type in /settings/light/0 endpoint
* [Shelly Dimmer/SL] Add attribute/parameter btn\_debounce to /settings/light/0 endpoint
* [Shelly Dimmer/SL] Add attribute/parameter min\_brightness to /settings endpoint
* [Shelly Dimmer/SL] Add attributes/parameters btn1\_longpush\_url, btn1\_shortpush\_url, btn2\_longpush\_url, btn2\_shortpush\_url to /settings/light/0 endpoint
* [Shelly Dimmer/SL] Add value toggle for parameter turn in /light/0 endpoint
* [Shelly Dimmer/SL] Publish new MQTT topics shellies/shellydimmer-\<deviceid\>/longpush/\<i\> and shellies/shellydimmer-\<deviceid\>/light/0/energy
* [Shelly EM] Publish new MQTT topics shellies/shellyem-\<deviceid\>/emeter/\<i\>/total and shellies/shellyem-\<deviceid\>/emeter/\<i\>/total\_returned
* [Shelly Flood] Add attributes/parameters flood\_detected\_url and flood\_gone\_url to /settings endpoint
v1.5.10
4.2.2020
* [All devices] Allow setting empty NTP server, this disables timekeeping on the device
v1.5.6
26.11.2019
* [All devices] Remove CoIoT actions
* [All devices] MQTT ID is now user-configurable (mqtt\_id)
* [All devices] Removed parameters mqtt\_will\_topic and mqtt\_will\_message from /settings endpoint
* [Shelly1, Shelly1PM, Shelly2, Shelly2.5] Add longpush and shortpush actions (longpush\_url, shortpush\_url)
* [Shelly2] Add voltage and current in power measurement info
* [Shelly Dimmer/SL] Add /settings/night\_mode endpoint, add fade\_rate command, add calibrate\_cancel command, add output activated/deactivated actions (out\_on\_url, out\_off\_url)
* [Shelly Dimmer/SL] Add Night Mode

Common HTTP API
==========

This section documents the HTTP API implemented by all Shelly devices, which defines their common traits:

* WiFi configuration
* Cloud settings
* HTTP authentication settings
* Firmware updates, identification and other system functions

For every Shelly device, one should consult this section, along with the chapter dedicated to the Shelly model in question.

HTTP dialect
----------

All properly formed requests return a JSON-encoded payload with an `application/json` MIME type. The meaning of values is described as **Attributes** for each documented resource.

Each resource may also accept a list of **Parameters** which should be supplied either as query-string in the URL or as `application/x-www-form-urlencoded` POST payload.

Error responses carry a 4xx HTTP response code and a `text/plain` response body, usually with an informative message for the type of error which occurred.

All resources except for `/shelly` will require Basic HTTP authentication when it is enabled via [`/settings/login`](#settings-login).

The HTTP method used for performing any of the requests below is intentionally ignored. Most endpoints will always return their specific JSON payload and perform actions if query parameters are specified.

Boolean parameters can be given as `1`, `y`, `Y`, `t`, `T` or case-insensitive `true` for true, any other value will be interpreted as false.

`/shelly`
----------

```
GET /shelly

{
    "type": "SHSW-21",
    "mac": "5ECF7F1632E8",
    "auth": true,
    "fw": "20161223-111304/master@2bc16496",
    "longid": 1,
    "discoverable": true
}

```

Provides basic information about the device. It does not require HTTP authentication, even if authentication is enabled globally. This endpoint can be used in conjunction with mDNS for device discovery and identification. It accepts no parameters.

### Attributes ###

|Attribute| Type |                                            Description                                             |
|---------|------|----------------------------------------------------------------------------------------------------|
| `type`  |string|                                      Shelly model identifier                                       |
|  `mac`  |string|                                     MAC address of the device                                      |
| `auth`  | bool |                            Whether HTTP requests require authentication                            |
|  `fw`   |string|                                      Current firmware version                                      |
|`longid` |number|`1` if the device identifies itself with its full MAC address; `0` if only the last 3 bytes are used|

`/settings`
----------

```
GET /settings

{
    "device": {
        "type": "SHSW-21",
        "mac": "16324CAABBCC",
        "hostname": "shelly1-B929CC"
    },
    "wifi_ap": {
        "enabled": false,
        "ssid": "shellyMODEL-16324CAABBCC",
        "key": ""
    },
    "wifi_sta": {
        "enabled": true,
        "ssid": "Castle",
        "ipv4_method": "dhcp",
        "ip": null,
        "gw": null,
        "mask": null,
        "dns": null
    },
    "wifi_sta1" : { ... },
    "ap_roaming": {
        "enabled": false,
        "threshold": -70
    },
    "mqtt": {
        "enable": false,
        "server": "192.168.33.3:1883",
        "user": "",
        "id": "shelly1-B929CC",
        "reconnect_timeout_max": 60,
        "reconnect_timeout_min": 2,
        "clean_session": true,
        "keep_alive": 60,
        "max_qos": 0,
        "retain": false,
        "update_period": 30
    },
    "coiot": {
        "enabled": true,
        "update_period": 15,
        "peer": ""
    },
    "sntp": {
        "server": "time.google.com",
        "enabled": true
    },
    "login": {
        "enabled": false,
        "unprotected": false,
        "username": "admin"
    },
    "pin_code": "123456",
    "name": "shellyMODEL-16324CAABBCC",
    "fw": "20170427-114337/master@79dbb397",
    "discoverable": true,
    "build_info": {
        "build_id": "20191112-140800",
        "build_timestamp": "2019-11-12T14:08:00Z",
        "build_version": "1.0"
    },
    "cloud": {
        "enabled": true,
        "connected": true
    },
    "timezone": "Europe/Sofia",
    "lat": 42.1234,
    "lng": 24.5678,
    "tzautodetect": true,
    "tz_utc_offset": 0,
    "tz_dst": false,
    "tz_dst_auto": true,
    "time": "16:40",
    "unixtime": 0,
    "led_status_disable": false,
    "debug_enable": false,
    "allow_cross_origin": false,
    "wifirecovery_reboot_enabled": true
}

```

Represents device configuration: all devices support a set of common features which are described here. Look at the device-specific `/settings` endpoint to see how each device extends it.

To configure timezone and location (for sunrise/sunset calculation) manually, set `tzautodetect` to `false`, so that custom values for `lat`, `lng` and `timezone` take effect. For a list of supported timezones, please fetch

<https://api.shelly.cloud/timezone/tzlist>

### Attributes ###

|          Attribute          | Type |                                                                                                     Description                                                                                                     |
|-----------------------------|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        `device.type`        |string|                                                                                               Device model identifier                                                                                               |
|        `device.mac`         |string|                                                                                      MAC address of the device in hexadecimal                                                                                       |
|      `device.hostname`      |string|                                                                                                   Device hostname                                                                                                   |
|          `wifi_ap`          | hash |                                                                   WiFi access point configuration, see [`/settings/ap`](#settings-ap) for details                                                                   |
|         `wifi_sta`          | hash |                                                                     WiFi client configuration. See [`/settings/sta`](#settings-sta) for details                                                                     |
|         `wifi_sta1`         | hash |                                                               Alternative WiFi client configuration. See [`/settings/sta`](#settings-sta) for details                                                               |
|    `ap_roaming.enabled`     | bool |                                                                                               AP roaming enabled flag                                                                                               |
|   `ap_roaming.threshold`    |number|                                                                                             AP roaming threshold, `dBm`                                                                                             |
|           `mqtt`            | hash |                                                                                           Contains MQTT-related settings                                                                                            |
|       `coiot.enabled`       | bool |                                                                                                 CoIoT enabled flag                                                                                                  |
|    `coiot.update_period`    |number|                                                                                        Update period of CoIoT messages, `s`                                                                                         |
|        `coiot.peer`         |string|                                                                                CoIoT peer (in format `ip:port`, empty means `mcast`)                                                                                |
|        `sntp.server`        |string|                                                                                                  Time server host                                                                                                   |
|       `sntp.enabled`        | bool |                                                                                                  SNTP enabled flag                                                                                                  |
|           `login`           | hash |Credentials used for HTTP Basic authentication for the REST interface. If `login.enabled` is `true` clients must include an `Authorization: Basic ...` HTTP header with valid credentials when performing TP requests|
|         `pin_code`          |string|                                                                                             Current generated PIN code                                                                                              |
|           `name`            |string|                                                                                              Unique name of the device                                                                                              |
|            `fw`             |string|                                                                                                 Current FW version                                                                                                  |
|       `discoverable`        | bool |                                                                                       Device discoverable (i.e. visible) flag                                                                                       |
|        `build_info`         | hash |                                                                                                     Build info                                                                                                      |
|       `cloud.enabled`       | bool |                                                                                                 Cloud enabled flag                                                                                                  |
|      `cloud.connected`      | bool |                                                                                                Cloud connected flag                                                                                                 |
|         `timezone`          |string|                                                                                                 Timezone identifier                                                                                                 |
|            `lat`            |number|                                                                                Degrees latitude in decimal format, South is negative                                                                                |
|            `lng`            |number|                                                                             Degrees longitude in decimal fomrat, between -180° and 180°                                                                             |
|       `tzautodetect`        | bool |                                                                                            Timezone auto-detect enabled                                                                                             |
|       `tz_utc_offset`       |number|                                                                                                     UTC offset                                                                                                      |
|          `tz_dst`           | bool |                                                                                                Daylight saving time                                                                                                 |
|        `tz_dst_auto`        | bool |                                                                                          Auto update daylight saving time                                                                                           |
|           `time`            |string|                                                                                       Current time in HH:MM format if synced                                                                                        |
|         `unixtime`          |number|                                                                                       Unix timestamp if synced; `0` otherwise                                                                                       |
|    `led_status_disable`     | bool |                                      **For Dimmer 1/2, DW2, i3, RGBW2, Plug, Plug S, EM, 3EM, 1L, 1PM, 2.5 and Button1** Whether LED indication for network status is enabled                                       |
|          `fw_mode`          |string|                                                       Current firmware mode, only for devices where this is changeable (e.g. Shelly RGBW2 Color/RGBW2 White)                                                        |
|       `debug_enable`        | bool |                                                                                           Debug file logger enabled flag                                                                                            |
|    `allow_cross_origin`     | bool |                                                                                   HTTP Cross-Origin Resource Sharing allowed flag                                                                                   |
|`wifirecovery_reboot_enabled`| bool |                                      Whether WiFi-Recovery reboot is enabled. Only applicable for Shelly 1/1PM, Shelly 2, Shelly 2.5, Shelly Plug/PlugS, Shelly EM, Shelly 3EM                                      |

### Parameters ###

|          Parameter          | Type |                                                                                     Description                                                                                      |
|-----------------------------|------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           `reset`           | bool |                                                                      Will perform a factory reset of the device                                                                      |
|    `ap_roaming_enabled`     | bool |                                                                              Enable/disable AP roaming                                                                               |
|   `ap_roaming_threshold`    |number|                                                                           Set AP roaming threshold, `dBm`                                                                            |
|        `mqtt_enable`        | bool |                                                                          Enable connecting to a MQTT broker                                                                          |
|        `mqtt_server`        |string|                                                                 MQTT broker IP address and port, ex. `10.0.0.1:1883`                                                                 |
|    `mqtt_clean_session`     | bool |                                                                               MQTT clean session flag                                                                                |
|        `mqtt_retain`        | bool |                                                                                   MQTT retain flag                                                                                   |
|         `mqtt_user`         |string|                                                                 MQTT username, leave empty to disable authentication                                                                 |
|         `mqtt_pass`         |string|                                                                                    MQTT password                                                                                     |
|          `mqtt_id`          |string|MQTT ID -- by default this has the form `<shellymodel>-<deviceid>` e.g. `shelly1-B929CC`. If you wish to use custom a MQTT ID, it is recommended that it doesn't exceed 25 characters.|
|`mqtt_reconnect_timeout_max` |number|                                                                       Maximum interval for reconnect attempts                                                                        |
|`mqtt_reconnect_timeout_min` |number|                                                                       Minimum interval for reconnect attempts                                                                        |
|      `mqtt_keep_alive`      |number|                                                                          MQTT keep alive period in seconds                                                                           |
|    `mqtt_update_period`     |number|                                                                      Periodic update in seconds, `0` to disable                                                                      |
|       `mqtt_max_qos`        |number|                                                                          Max value of QOS for MQTT packets                                                                           |
|       `coiot_enable`        | bool |                                                                                 Enable/disable CoIoT                                                                                 |
|    `coiot_update_period`    |number|                                                                     Update period of CoIoT messages `15..65535s`                                                                     |
|        `coiot_peer`         |string|                        Set to either `mcast` to switch CoIoT to multicast or to `ip[:port]` to switch CoIoT to unicast (`port` is optional, default is 5683)                         |
|        `sntp_server`        |string|                       Time server host to be used instead of the default `time.google.com`. An empty value disables timekeeping and requires reboot to apply.                        |
|           `name`            |string|                                                                            User-configurable device name                                                                             |
|       `discoverable`        | bool |                                                               Set whether device should be discoverable (i.e. visible)                                                               |
|         `timezone`          |string|                                                                                 Timezone identifier                                                                                  |
|            `lat`            |number|                                                                Degrees latitude in decimal format, South is negative                                                                 |
|            `lng`            |number|                                                                  Degrees longitude in decimal format, `-180°..180°`                                                                  |
|       `tzautodetect`        | bool |                                          Set this to `false` if you want to set custom geolocation (`lat` and `lng`) or custom `timezone`.                                           |
|       `tz_utc_offset`       |number|                                                                                      UTC offset                                                                                      |
|          `tz_dst`           |number|                                                                              Daylight saving time `0/1`                                                                              |
|        `tz_dst_auto`        |number|                                                                        Auto update daylight saving time `0/1`                                                                        |
|    `led_status_disable`     | bool |                         **For Dimmer 1/2, DW2, i3, RGBW2, Plug, Plug S, EM, 3EM, 1L, 1PM, 2.5 and Button1** Enable/Disable LED indication for network status                         |
|       `debug_enable`        | bool |                                                                           Enable/disable debug file logger                                                                           |
|    `allow_cross_origin`     | bool |                                                                   Allow/forbid HTTP Cross-Origin Resource Sharing                                                                    |
|`wifirecovery_reboot_enabled`| bool |                        Enable/disbale WiFi-Recovery reboot. Only applicable for Shelly 1/1PM, Shelly 2, Shelly 2.5, Shelly Plug/PlugS, Shelly EM, Shelly 3EM                         |

`/settings/ap`
----------

```
GET /settings/ap

{
    "enabled": false,
    "ssid": "shellyswitch-163248",
    "key": ""
}

```

Provides information about the current WiFi AP configuration and allows changes. The returned document is identical to the one returned by `/settings` in the `wifi_ap` key. Shelly devices do not allow the SSID for AP WiFi mode to be changed.

Parameters are applied immediately. Setting the `enabled` flag for AP mode to `1` will automatically disable STA mode.

### Attributes ###

|Attribute| Type |                        Description                        |
|---------|------|-----------------------------------------------------------|
|`enabled`| bool |                 Whether AP mode is active                 |
| `ssid`  |string|              SSID created by the device's AP              |
|  `key`  |string|WiFi password required for association with the device's AP|

### Parameters ###

|Parameter| Type |                        Description                        |
|---------|------|-----------------------------------------------------------|
|`enabled`| bool |      Set to `1` to return the device to AP WiFi mode      |
|  `key`  |string|WiFi password required for association with the device's AP|

`/settings/sta`
----------

```
GET /settings/sta

{
    "enabled": true,
    "ssid": "Castle",
    "ipv4_method": "dhcp",
    "ip": null,
    "gw": null,
    "mask": null,
    "dns": null
}

```

Provides information about the current WiFi Client mode configuration and allows changes. The returned document is identical to the one returned by `/settings` in the `wifi_sta` key.

Parameters are applied immediately. Setting the `enabled` flag for STA mode to `1` will automatically disable AP mode.

An identical resource is available at `/settings/sta1`. This allows for devices to have a second WiFi STA configuration for fallback, and will cycle between the two when the one currently selected becomes unavailable.

### Attributes ###

|  Attribute  | Type |                     Description                     |
|-------------|------|-----------------------------------------------------|
|  `enabled`  | bool |             Whether STA mode is active              |
|   `ssid`    |string|     SSID of STA the device will associate with      |
|`ipv4_method`|string|                 `dhcp` or `static`                  |
|    `ip`     |string|    Local IP address if `ipv4_method` is `static`    |
|    `gw`     |string|Local gateway IP address if `ipv4_method` is `static`|
|   `mask`    |string|          Mask if `ipv4_method` is `static`          |
|    `dns`    |string|      DNS address if `ipv4_method` is `static`       |

### Parameters ###

|  Parameter  | Type |                        Description                         |
|-------------|------|------------------------------------------------------------|
|  `enabled`  | bool |        Set to `1` to make STA the current WiFi mode        |
|   `ssid`    |string|              The WiFi SSID to associate with               |
|    `key`    |string|The password required for associating to the given WiFi SSID|
|`ipv4_method`|string|                     `dhcp` or `static`                     |
|    `ip`     |string|       Local IP address if `ipv4_method` is `static`        |
|  `netmask`  |string|             Mask if `ipv4_method` is `static`              |
|  `gateway`  |string|   Local gateway IP address if `ipv4_method` is `static`    |
|    `dns`    |string|          DNS address if `ipv4_method` is `static`          |

Sinve v.1.7.0, setting a static IP only requires `netmask` to be specified, `gateway` can be left empty.

Please note that cloud must be disabled manually before setting a static IP config without a `gateway` and enabled manually when switching back to `dhcp` config ([`/settings/cloud`](#settings-cloud)).

`/settings/login`
----------

```
GET /settings/login

{
    "enabled": false,
    "unprotected": false,
    "username": "admin"
}

```

```
GET /settings/login?enabled=1&username=boss&password=thebigone

{
    "enabled": true,
    "unprotected": false,
    "username": "boss"
}

```

HTTP authentication configuration: `enabled` flag, credentials. `unprotected` is initially false and is used by the user interface to show a warning when auth is disabled. If the user wants to keep using Shelly without a password, they can set `unprotected` to hide the warning.

### Attributes ###

|  Attribute  | Type |              Description              |
|-------------|------|---------------------------------------|
|  `enabled`  | bool |Whether HTTP authentication is required|
|`unprotected`| bool |Whether the user is aware of the risks |
| `username`  |string|               Username                |

In order to prevent security issues (e.g. when forwarding logs to 3rd parties), since v1.7.0 the `password` attribute for login protected devices is no longer returned on the API call.

### Parameters ###

|  Parameter  | Type |             Description              |
|-------------|------|--------------------------------------|
|  `enabled`  | bool |Whether to require HTTP authentication|
|`unprotected`| bool |Whether the user is aware of the risks|
| `username`  |string|       Length between 1 and 50        |
| `password`  |string|       Length between 1 and 50        |

`/settings/cloud`
----------

```
GET /settings/cloud?enabled=1

{
    "enabled": true
}

```

Can set the `enabled` (connect to cloud) flag. When set, Shelly will keep a secure connection to Allterco's servers and allow monitoring and control from anywhere.

`/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [
          "http://192.168.1.4/on",
          "http://192.168.1.5/on"
        ],
        "enabled": true
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "over_power_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      },
      {
        "index": 1,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      },
      {
        "index": 2,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      }
    ],
    "under_power_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      },
      {
        "index": 1,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      },
      {
        "index": 2,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      }
    ]
  }
}

```

### Attributes ###

|Attribute| Type |     Description     |
|---------|------|---------------------|
| `index` |number|   Channel number    |
| `name`  |string|     Action name     |
|`enabled`| bool |Enable/disable action|
|`urls[]` |string|     Action URL      |

### Parameters ###

|Parameter| Type |     Description     |
|---------|------|---------------------|
| `index` |number|   Channel number    |
| `name`  |string|     Action name     |
|`enabled`| bool |Enable/disable action|
|`urls[]` |string|     Action URL      |

Since v1.8.0 devices support multiple actions.
Max number of URLs per action is 5.
Max URLs length is 256.

### Examples: ###

* Setting two URLs for `out_on_url` action on channel 0:

`http://192.168.33.1/settings/actions?index=0&name=out_on_url&enabled=true&urls[]=http://192.168.1.4/on&urls[]=http://192.168.1.5/on`

* Disable only action `out_on_url` on channel 0:

`http://192.168.33.1/settings/actions?index=0&name=out_on_url&enabled=false`

* Delete URLs for action `out_on_url` action on channel 0:

`http://192.168.33.1/settings/actions?index=0&name=out_on_url&urls[]=`

* Some devices have additional parameters which may be set along with actions.
  Example: Setting URLs and `over_power_url_threshold` parameter for action `over_power_url` on channel 0:

`http://192.168.33.1/settings/actions?index=0&name=over_power_url&enabled=true&urls[]=192.168.1.4/overpower&urls[]=192.168.1.5/overpower&over_power_url_threshold=100`

`/status`
----------

```
GET /status

{
    "wifi_sta": {
        "connected": true,
        "ssid": "Castle",
        "ip": "192.168.2.65",
        "rssi": -54
    },
    "cloud": {
        "enabled": false,
        "connected": false
    },
    "mqtt": {
        "connected": false
    },
    "time": "17:42",
    "unixtime": 0,
    "serial": 1,
    "has_update": true,
    "mac": "98F4ABB929CC",
    "update": {
        "status": "pending",
        "has_update": true,
        "new_version": "20200320-123430/v1.6.2@514044b4",
        "old_version": "20200320-123430/v1.6.2@514044b4"
    },
    "ram_total": 50648,
    "ram_free": 38376,
    "ram_lwm": 32968,
    "fs_size": 233681,
    "fs_free": 174194,
    "uptime": 39
}

```

Encapsulates current device status information. While settings can generally be modified and don't react to the environment, this endpoint provides information about transient data which may change due to external conditions.

### Attributes ###

|   Attribute    | Type |                                     Description                                     |
|----------------|------|-------------------------------------------------------------------------------------|
|   `wifi_sta`   | hash |                        Current status of the WiFi connection                        |
| `wifi_sta.ip`  |string|                IP address assigned to this device by the WiFi router                |
|    `cloud`     | hash |                           Current cloud connection status                           |
|`mqtt.connected`| bool |                    MQTT connection status, when MQTT is enabled                     |
|     `time`     |string|                   The current hour and minutes, in `HH:MM` format                   |
|   `unixtime`   |number|                       Unix timestamp if synced; `0` otherwise                       |
|    `serial`    |number|                                 Cloud serial number                                 |
|    `update`    | hash |Info whether newer firmware version is available, see [`/ota`](#ota) for more details|
|  `ram_total`   |number|                       Total amount of system memory in bytes                        |
|   `ram_free`   |number|                     Available amount of system memory in bytes                      |
|   `ram_lwm`    |number|                Minimal watermark of the system free memory in bytes                 |
|   `fs_size`    |number|                      Total amount of the file system in bytes                       |
|   `fs_free`    |number|                    Available amount of the file system in bytes                     |
|    `uptime`    |number|                             Seconds elapsed since boot                              |

`/reboot`
----------

```
GET /reboot

{}

```

When requested will cause a reboot of the device.

`/ota`
----------

```
GET /ota

{
    "status": "idle",
    "has_update": false,
    "new_version": "20200320-123430/v1.6.2@514044b4",
    "old_version": "20200320-123430/v1.6.2@514044b4"
}

```

Provides information about the device firmware version and the ability to trigger an over-the-air update.

### Attributes ###

|  Attribute   | Type |                            Description                             |
|--------------|------|--------------------------------------------------------------------|
|   `status`   |string|          One of `idle`, `pending`, `updating`, `unknown`           |
| `has_update` | bool |                   Whether an update is available                   |
|`new_version` |string|                     ID of new firmware version                     |
|`old_version` |string|                ID of old (current) firmware version                |
|`beta_version`|string|ID of beta firmware if one is available. This attribute is optional.|

### Parameters ###

|Parameter| Type |                  Description                   |
|---------|------|------------------------------------------------|
|  `url`  |string|     Run firmware update from specified URL     |
|`update` | bool |      Run firmware update from default URL      |
| `beta`  | bool |Run firmware update from beta URL (if available)|

`/ota/check`
----------

```
GET /ota/check

{
    "status": "ok"
}

```

Manual check for new firmware version.

### Attributes ###

|Attribute| Type |   Description   |
|---------|------|-----------------|
|`status` |string|`ok` or `running`|

`/wifiscan`
----------

```
GET /wifiscan

{
    "wifiscan": "done",
    "results": [
        {
            "ssid": "some_network_1",
            "auth": 4,
            "channel": 1,
            "bssid": "XXXXXXXXXXXX",
            "rssi": -70
        },
        {
            "ssid": "some_network_2",
            "auth": 3,
            "channel": 6,
            "bssid": "YYYYYYYYYYYY",
            "rssi": -83
        }
    ]
}

```

Only available when in AP mode. Starts a WiFi scan and provides information about found networks.

### Attributes ###

|        Attribute        | Type |                                         Description                                          |
|-------------------------|------|----------------------------------------------------------------------------------------------|
|       `wifiscan`        |string|               One of `failed`, `done`, `not AP mode`, `started`, `inprogress`                |
| `results.{index}.ssid`  |string|                                             SSID                                             |
| `results.{index}.auth`  |number|Auth mode: `0`=open, `1`=WEP, `2`=WPA PSK, `3`=WPA2 PSK, `4`=WPA WPA2 PSK, `5`=WPA2 ENTERPRISE|
|`results.{index}.channel`|number|                                           Channel                                            |
| `results.{index}.bssid` |string|                                         BSSID in hex                                         |
| `results.{index}.rssi`  |number|                                       Signal strength                                        |

`/debug/log`
----------

```
GET /debug/log

```

Retrieve debug log file 0

`/debug/log1`
----------

```
GET /debug/log1

```

Retrieve debug log file 1

`/cit/d`
----------

```
GET /cit/d

{
    "blk":[
        ...
    ],
    "sen":[
        ...
    ]
}

```

Get CoIoT description package over HTTP

`/sta_cache_reset`
----------

```
GET /sta_cache_reset

```

Reset STA cache: only applicable on devices which support STA caching (battery operated devices Shelly Door/Window 1/2, Shelly H&T, Shelly Smoke, Shelly Flood, Shelly Button1)

MQTT Support
==========

Shelly devices include basic MQTT support since version 1.3.0. While many device settings are only available over HTTP, MQTT allows for real-time monitoring and eases integration with external systems.

MQTT Configuration
----------

To configure a Shelly device for MQTT, set the connection parameters via the Shelly App, web interface or HTTP [`/settings`](#settings) endpoint. Note, that enabling MQTT will disable Allterco's cloud service. Shelly devices do not support secure MQTT connections.

Mandatory settings are:

* `mqtt_server` is your broker's `address:port`
* `mqtt_enable` needs to be set to `true`

In case authentication is required, `mqtt_user` and `mqtt_pass` must also be set. In certain scenarios, it may be desirable to set `mqtt_max_qos` and `mqtt_retain` to prevent loss of data.

By default, the device's MQTT ID is `<shellymodel>-<deviceid>`, for example `shelly1-B929CC`. The MQTT ID can be changed via the `mqtt_id` parameter in [`/settings`](#settings). If you wish to use custom a MQTT ID, it is recommended that it doesn't exceed 25 characters.

In order to apply the MQTT configuration, the device requires a reboot.

Availability and announces
----------

Since v1.4.3: on MQTT connect, Shellies will publish:

* an announce message on `shellies/announce` and, since v1.6.0, on `shellies/<shellymodel>-<deviceid>/announce`. The message is JSON-formatted and contains a list of attributes: `id`, `mode` (if applicable), `model`, `mac`, `ip`, `new_fw` (`true` when an update is available), `fw_ver` (contains the current firmware version);
* availability message on `shellies/<shellymodel>-<deviceid>/online` with payload `true`;
* complete current state. This is device specific and is described in detail for each device below.

Device state is reported periodically, every 30 seconds by default. This can be changed by setting a new period for updates: `mqtt_update_period` under [`/settings`](#settings). A value of `0` will disable periodic updates.

Default LWT topic and message are `shellies/<shellymodel>-<deviceid>/online`, `false`. If these are not set after a firmware upgrade -- perform a factory reset of the device.
The LWT topic is retained on user configuration (if the Retain flag is set). However, we do not recommend using retained MQTT messages.

Common MQTT commands
----------

Shellies support a set of commands published on `shellies/command` or `shellies/<shellymodel>-<deviceid>/command` to address an individual device:

* `announce` will trigger:
  * an announce packet by every Shelly connected to the broker on `shellies/announce` and, since v1.6.0, on `shellies/<shellymodel>-<deviceid>/announce`;
  * since v1.8.0, `shellies/<shellymodel>-<deviceid>/info` with the content of the http `/status` endpoint.

* `update` will cause all Shellies to publish their state;
* `update_fw` to perform a firmware update when one is available.

Each Shelly model exports it's own set of topics for monitoring and control, all structured under `/shellies/<shellymodel>-<deviceid>`. Please see the respective product docs for details on the protocol:

* [Shelly1/1PM](#shelly1-1pm-mqtt)
* [Shelly2](#shelly2-mqtt)
* [Shelly2.5](#shelly2-5-mqtt)
* [Shelly4Pro](#shelly4pro-mqtt)
* [Shelly Plug/Plug S](#shelly-plug-plugs-mqtt)
* [Shelly i3](#shelly-i3-mqtt)
* [Shelly Button1](#shelly-button1-mqtt)
* [Shelly Bulb](#shelly-bulb-mqtt)
* [Shelly Vintage](#shelly-vintage-mqtt)
* [Shelly Duo](#shelly-duo-mqtt)
* [Shelly RGBW2 Color](#shelly-rgbw2-color-mqtt)
* [Shelly RGBW2 White](#shelly-rgbw2-white-mqtt)
* [Shelly Dimmer/SL](#shelly-dimmer-sl-mqtt)
* [Shelly Sense](#shelly-sense-mqtt)
* [Shelly H&T](#shelly-h-amp-t-mqtt)
* [Shelly Smoke](#shelly-smoke-mqtt)
* [Shelly Flood](#shelly-flood-mqtt)
* [Shelly Door/Window](#shelly-door-window-mqtt)
* [Shelly Gas](#shelly-gas-mqtt)
* [Shelly EM](#shelly-em-mqtt)
* [Shelly 3EM](#shelly-3em-mqtt)

CoIoT Protocol
==========

The CoIoT protocol is yet another protocol for IoT communication and integration. CoIoT is based on [CoAP](https://tools.ietf.org/html/rfc7252) with some additions as new request code `0.30` for status publishing. All payloads are JSON encoded. All responses are piggyback sent with the acknowledgement to further simplify CoAP implementation.

Every CoIoT device is expected to handle a set of request URIs and generate responses in predefined format. Also every device is required to periodically send a multicast CoAP request with code `0.30` that describes it state.

Every CoAP request package and every response with payload should also carry some mandatory CoAP options (headers).

CoIoT protocol version
----------

CoIoT protocol version can be obtained from option 3332 `COIOT_OPTION_GLOBAL_DEVID` : `<devtype>#<devid>#<version>`

* Devices with **FW \< v1.8.0** will return version **1**, e.g.: `SHSW-1#A020A6146209#1`
* Devices with **FW \>= v1.8.0** will return version **2**, e.g.: `SHSW-1#A020A6146209#2`

Documentation for version 1 can be found here: [CoIoT for Shelly devices (rev 1.0) .pdf](docs/coiot/v1/CoIoT%20for%20Shelly%20devices%20(rev%201.0)%20.pdf)

The rest of this document is applicable for version 2.

CoIoT mandatory CoAP options
----------

Some non-standard CoAP options are required to be transmitted to help quickly identify the remote device and determine if further processing is needed. The options are numbered with the help of these C/C++ preprocessor macros:

```
#define COIOT_OPTION_BASE               3332 //non critical, save to forward, no cache key
#define COIOT_OPTION_INCR               8
#define COIOT_OPTION_N(n)               (COIOT_OPTION_BASE+(COIOT_OPTION_INCR)*(n))

#define COIOT_OPTION_GLOBAL_DEVID       COIOT_OPTION_N(0)
#define COIOT_OPTION_MGR_GLOBAL_NBASE   1
#define COIOT_OPTION_STATUS_NBASE       10
#define COIOT_OPTION_STATUS_VALIDITY    COIOT_OPTION_N(COIOT_OPTION_STATUS_NBASE+0)
#define COIOT_OPTION_STATUS_SERIAL      COIOT_OPTION_N(COIOT_OPTION_STATUS_NBASE+1)
#define COIOT_OPTION_MGR_STATUS_NBASE   20

```

To follow the CoAP standard, options are numbered above 2048 where proprietary options should reside. LS Bits carry some CoAP proxy flags so we guard them with spacing the numbers with increment of 8.

### COIOT\_OPTION\_GLOBAL\_DEVID ###

First defined option is `COIOT_OPTION_GLOBAL_DEVID`. This is a global option and must be present in all CoIoT packages with request or payload. Its value is a string in format `<devtype>#<devid>#<version>` for example `SHSEN-1#4B3F9E#1` The whole option should be less than 50 bytes.

Other mandatory options are `COIOT_OPTION_STATUS_VALIDITY` and `COIOT_OPTION_STATUS_SERIAL`. They are mandatory only in status responses or publishes.

### COIOT\_OPTION\_STATUS\_VALIDITY ###

`COIOT_OPTION_STATUS_VALIDITY` is a `uint16_t` in network byte order (big endian) that states the maximal time between this and the next status publish. This way a device can state its report interval. If a report is not received from this device after the interval has passed the device should be considered offline. The LS bit of this option controls how the value is scaled:

* If the LS bit is 0, the value is number of 1/10 of seconds in the validity period, so 2 is 0.2 seconds, 10 is a second, 600 is a minute, 65534 is 109 minutes and 13 seconds.
* If the LS bit is 1, the value is number of 4 seconds interval in the whole interval. So 3 is 12 seconds, 11 is 44 seconds and 65535 is more than 3 days.

### COIOT\_OPTION\_STATUS\_SERIAL ###

This option is mandatory in status response and publishes. It is a `uint16_t` in network byte order which indicates a change in the status report. When a new status report is handled, all payload processing can be skipped if the serial number does not change from the last processed payload. The value 0 is reserved and should not be sent. This allows easy initialization in the receiving devices.

Serial will always be incremented monotonically (i.e. +1). If you have a packet with serial "4" and the next is with serial "6", it means "5" got lost and didn't reach you.

CoIoT device description (/cit/d)
----------

Every device should response to CoAP GET request with URI `/cit/d` and return a JSON payload describing the device.

Note: since v1.10.0 all devices support an HTTP endpoint `/cit/d` which allows to retrieve the same CoIoT description package as the CoAP GET request.

Throughout the description all `<id>` values should be non-overlapping integers that are used as unique identificators of blocks and sensors.

Toplevel object should look like:

```
{
    "blk": [...],
    "sen": [...]
}

```

### `blk` array ###

`blk` array should hold list of all "blocks" of the device. Each device should have at least one block. For example if your device exposes just a few sensors it needs just one block, but if you have a multi channel relay you should define a block for each relay. Each sensor should be linked to one or many blocks to help users better understand what is measured in more complex devices.

`blk` elements should be objects with structure:

```
{
    "I": id,
    "D": description
}

```

for example:

```
"blk":[
    {
        "I":1,
        "D":"relay_0"
    },
    {
        "I":2,
        "D":"relay_1"
    },
    {
        "I":3,
        "D":"device"
    }
]

```

### "I":id (mandatory) ###

* `<id>` is recommended to start from 1 for the first declared block and increment monotonically (i.e. +1) for subsequent blocks, but in general it's not forbidden to declare blocks with arbitrary `<id>`s.

### "D":description (mandatory) ###

* `<description>` is recommended to be one word, camelCase or camelCase\_N (where N is some number), but in general it's not forbidden to have longer descriptions.
* `“device”` block will always be present.

### `sen` array ###

`sen` array should hold a list of all sensors and states in the device. These should be objects with structure:

```
{
    "I": id,
    "T": type,
    "D": description,
    "U": unit,
    "R": range,
    "L": links
}

```

for example:

```
"sen":[
    {
        "I":1101,
        "T":"S",
        "D":"output",
        "R":"0/1",
        "L":1
    },
    {
        "I":1201,
        "T":"S",
        "D":"output",
        "R":"0/1",
        "L":2
    }
]

```

Device descriptions will strive to provide all properties supported by the device, even if they are currently
disabled/unavailable on the specific device. For example, a Shelly1 will always include a description of properties related to external (add-on) sensors, even if they are not currently attached (but of course, in this case they will be hidden from the status packet).

### “I”:id (mandatory) ###

* All devices will follow an internal scheme to generate `<id>`s for properties (i.e. specific `<id>`s map to specific properties), but this should NOT be relied upon. You should assume `<id>`s have no external meaning and treat them just as numbers to precisely "name" a property.

### “T”:type (mandatory) ###

* `<type>` will always be 1 to 3 characters, only capital letters.

For now the following types are declared:

|`<type>`|            Description            |
|--------|-----------------------------------|
|  “A”   |               Alarm               |
|  “B”   |           Battery level           |
|  “C”   |           Concentration           |
|  “E”   |              Energy               |
|  “EV”  |               Event               |
| “EVC”  |           Event counter           |
|  “H”   |             Humidity              |
|  “I”   |              Current              |
|  “L”   |            Luminosity             |
|  “P”   |               Power               |
|  “S”   |Status (catch-all if no other fits)|
|  “T”   |            Temperature            |
|  “V”   |              Voltage              |

`“EV”` (Event) and `“EVC”` (Event counter) are newly introduced types to be able to communicate the occurrence of events. Such events are for example shortpush/longpush of buttons – devices will send a property of type `“EV”` to denote the exact event type (“S” = shortpush, “L” = longpush), and a property of type `“EVC”` that will increment its value when a new event occurs (e.g. to be able to know that two consecutive longpushes are actually two separate events).

### “D”:description (mandatory) ###

* `<description>` is recommended to be one word, camelCase or camelCase\_N (where N is some number) - e.g. `“output”`, `“rollerPos”`, but in general it's not forbidden to have longer descriptions (consider them "free text" - for a human reading the
  description to get a better understanding of the property).

### “U”:unit (optional) ###

* `<unit>` is a newly introduced optional attribute. If it’s necessary to specify a dimension for a property, it will be done here, not in `<type>` or `<description>`.

For now the following units are declared:

|`<unit>`|   Description   |
|--------|-----------------|
|  “W”   |      Watts      |
| “Wmin” |  Watt minutes   |
|  “Wh”  |   Watt hours    |
|  “V”   |      Volts      |
|  “A”   |     Amperes     |
|  “C”   |     Celsius     |
|  “F”   |   Fahrenheit    |
|  “K”   |     Kelvin      |
| “deg”  | degrees (angle) |
| “lux”  |       Lux       |
| “ppm”  |parts per million|
|  “s”   |     seconds     |
| "pct"  |     percent     |

### “R”:range (optional) ###

`<range>` is allowed to be either:

* a single string, specifying normal range in form `"from/to"`, `"valueX/valueY/.../valueZ"` or `"<I|U><8|16|32>"`, the latter showing expected sIgned or Unsigned integer size
* an array of strings, specifying normal range and invalid value in form [`"<normal>"`,`"<invalid>"`]. `"<invalid>"` = the value you'll get if "real" data is unavailable at the moment (e.g. sensor broke)

For example:

* “0/100” - normal range is from 0 to 100; no invalid value
* “obstacle/overpower/safety\_switch” - normal range is “obstacle”, “overpower” or “safety\_switch”; no invalid value
* [“0/255”,”999”] - normal range is from 0 to 255; invalid value is 999
* [“U16”,”-1”] - normal range is uint16, invalid value is -1

### “L”:links (mandatory) ###

* `<links>` can be a single integer or array of integers with `<id>`s of device blocks to which a property relates.

CoIoT device status (/cit/s)
----------

Every device should respond to CoAP GET request with URI `/cit/s` and return a JSON payload describing the device. Every device should periodically publish its status using multicast packet in the form of non-confirmable request with code `0.30` and request path `/cit/s`. This code is non-standard CoAP code and all CoAP compliant servers should silently ignore it. Throughout the status report all `<id>` values should match sensors ids from the device description. The JSON payload should follow the form:

```
{
    "G":[
            [0,id,value],
            [0,id,value],
            ...
        ]
}

```

for example:

```
{
    "G":[
            [0,1101,1],
            [0,1104,136],
            ...
        ]
}

```

The `G` key stands for `Generic`. Currently all sensor values are generic and non-encrypted. Future extensions of the protocol might add `P` for `Private` and define some encryption scheme.

The `0` in the sensor tuples stands for the channel number. All sensors are required to be emitted in channel `0`. Future extensions of the protocol might define a way for the users to define extra mapping for sensors to channels that will be added to the status after the values from channel `0`. This will allow for easy reconfiguration of peer to peer network. For example, a multizone alarm system can be configured to react based on channel number activity and not to have to explicitly list every sensor on every siren. Currently the first position in the sensor tuple is reserved and should be `0`.

The second position is for the sensor `<id>`, and the third is for the sensor's current `<value>`.

CoIoT list of properties
----------

Below is a list of all properties currently reported by the devices with CoIoT protocol version 2, along with short comments on their meaning. Please bear in mind that this is just a generalized example – attributes such as e.g. `<range>` are device specific.

* [CoIoT v2 property list](docs/coiot/v2/coiot_v2_property_list.ods)

CoIoT examples
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`) are provided separetely for each device:

* [Shelly1/1PM](#shelly1-1pm-coiot)
* [Shelly2](#shelly2-coiot)
* [Shelly2.5](#shelly2-5-coiot)
* [Shelly Plug/Plug S](#shelly-plug-plugs-coiot)
* [Shelly i3](#shelly-i3-coiot)
* [Shelly Button1](#shelly-button1-coiot)
* [Shelly Bulb](#shelly-bulb-coiot)
* [Shelly Vintage](#shelly-vintage-coiot)
* [Shelly Duo](#shelly-duo-coiot)
* [Shelly RGBW2 Color](#shelly-rgbw2-color-coiot)
* [Shelly RGBW2 White](#shelly-rgbw2-white-coiot)
* [Shelly Dimmer/SL](#shelly-dimmer-sl-coiot)
* [Shelly H&T](#shelly-h-amp-t-coiot)
* [Shelly Smoke](#shelly-smoke-coiot)
* [Shelly Flood](#shelly-flood-coiot)
* [Shelly Door/Window](#shelly-door-window-coiot)
* [Shelly Gas](#shelly-gas-coiot)
* [Shelly EM](#shelly-em-coiot)
* [Shelly 3EM](#shelly-3em-coiot)

Shelly1 / Shelly1PM
==========

Shelly1/PM: Overview
----------

Shelly1 is the smallest intelligent Wi-Fi power switch on the market today. Visit the product page for detailed description and User Manual:

<https://shelly.cloud/products/shelly-1-smart-home-automation-relay/>

Shelly1PM also includes energy metering:

<https://shelly.cloud/shelly-1pm-wifi-smart-relay-home-automation/>

Commands to turn the relay on or off can come from:

* A physical button
* HTTP request, trough the local web interface
* A command sent via the cloud or MQTT
* A weekly-schedule event or a sunrise/sunset-generated event
* **Shelly1PM only:** Overpower condition will turn the relay OFF

Shelly1/PM supports up to 18 schedule rules.

### Factory Reset ###

If the web interface of the device cannot be accessed, settings can be brought back to default by switching ON and OFF 5 times the physical switch connected to the device, within the first minute after a reboot or power-on.

### About the device ###

Shelly1/1PM supports the **ON** and **OFF** commands which control the coil of a 16A 250VAC relay.

Shelly1/1PM also supports `auto_on` and `auto_off` settings -- these are timers in seconds which will turn the device ON or OFF when it has been turned OFF or ON respectively, from either a physical button or network command. Thus, the user can set a limit for how long the device can be **ON** or **OFF**.

Upon power-on, output is initialized using one of 4 available strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly

To control Shelly1/1PM, use these resources:

* [`/settings/relay/0`](#shelly1-1pm-settings-relay-0) to configure behavior
* [`/relay/0`](#shelly1-1pm-relay-0) to control and monitor

Shelly1/1PM: MQTT
----------

Shelly1 and Shelly1PM uses the following topics, where `<model>` is either `shelly1` or `shelly1pm`:

* `shellies/<model>-<deviceid>/relay/0` to report status: `on`, `off` or `overpower` (the latter only for Shelly1PM)
* `shellies/<model>-<deviceid>/relay/0/command` accepts `on`, `off` or `toggle` and applies accordingly
* `shellies/<model>-<deviceid>/input/0` reports the state of the `SW` terminal
* `shellies/<model>-<deviceid>/longpush/0` reports `longpush` state as `0` (shortpush) or `1` (longpush)
* `shellies/<model>-<deviceid>/input_event/0` reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly1-1pm-status) for details

Shelly1PM adds:

* `shellies/shelly1pm-<deviceid>/relay/0/power` reports instantaneous power in Watts
* `shellies/shelly1pm-<deviceid>/relay/0/energy` reports an incrementing energy counter in Watt-minute
* `shellies/shelly1pm-<deviceid>/temperature` reports internal device temperature in °C
* `shellies/shelly1pm-<deviceid>/temperature_f` reports internal device temperature in °F
* `shellies/shelly1pm-<deviceid>/overtemperature` reports `1` when device has overheated, normally `0`
* `shellies/shelly1pm-<deviceid>/temperature_status` reports `Normal`, `High`, `Very High`
* `shellies/shelly1pm-<deviceid>/relay/0/overpower_value` reports the value in Watts, on which an overpower condition is detected

If Shelly1/1PM is equipped with a [temperature add-on](https://shop.shelly.cloud/temperature-sensor-addon-for-shelly-1-1pm-wifi-smart-home-automation#312), following topics are published as well:

For add-ons with DS1820 sensors:

* `shellies/<model>-<deviceid>/ext_temperature/<i>` where `<i>` is the sensor id `[0,1,2]`: reports temperature in °C, `999` if invalid
* `shellies/<model>-<deviceid>/ext_temperature_f/<i>` where `<i>` is the sensor id `[0,1,2]`: reports temperature in °F, `999` if invalid

For add-ons with a DHT22 sensor, in addition to the temperature topic above, a humidity topic is published too:

* `shellies/<model>-<deviceid>/ext_humidity/0` reports humidity in percent, `999` if invalid

Shelly1/1PM also provide aggregated topics which contain data from all sensors along with their hardware IDs. They publish a JSON payload similar to the one in [`/status`](#shelly1-1pm-status)

* `shellies/<model>-<deviceid>/ext_temperatures`

```
{
    "0":{"hwID":"XXXXXXXX","tC":20.5},
    "1":{"hwID":"YYYYYYYY","tC":21.5},
    "2":{"hwID":"ZZZZZZZZ","tC":22.5}
}

```

* `shellies/<model>-<deviceid>/ext_temperatures_f`

```
{
    "0":{"hwID":"XXXXXXXX","tF":68.9},
    "1":{"hwID":"YYYYYYYY","tF":70.7},
    "2":{"hwID":"ZZZZZZZZ","tF":72.5}
}

```

* `shellies/<model>-<deviceid>/ext_humidities`

```
{
    "0":{"hwID":"XXXXXXXX","hum":50}
}

```

Shelly1/1PM: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

Shelly1:

* [Shelly 1 SHSW-1 no-addon](docs/coiot/v2/examples/Shelly%201%20SHSW-1%20no-addon)
* [Shelly 1 SHSW-1 with-ds1820](docs/coiot/v2/examples/Shelly%201%20SHSW-1%20with-ds1820)
* [Shelly 1 SHSW-1 with-dht22](docs/coiot/v2/examples/Shelly%201%20SHSW-1%20with-dht22)

Shelly 1PM:

* [Shelly 1PM SHSW-PM no-addon](docs/coiot/v2/examples/Shelly%201PM%20SHSW-PM%20no-addon)
* [Shelly 1PM SHSW-PM with-ds1820](docs/coiot/v2/examples/Shelly%201PM%20SHSW-PM%20with-ds1820)
* [Shelly 1PM SHSW-PM with-dht22](docs/coiot/v2/examples/Shelly%201PM%20SHSW-PM%20with-dht22)

Shelly1/1PM: `/settings`
----------

```
GET /settings (Shelly1PM without temperature add-on, with low-power switch add-on)

{
    "factory_reset_from_switch": true,
    "max_power": 2000,
    "supply_voltage": 0,
    "power_correction": 1,
    "mode": "relay",
    "led_status_disable": false,
    "longpush_time": 1000,
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "btn_off_url",
            "out_on_url",
            "out_off_url",
            "longpush_url",
            "shortpush_url",
            "lp_on_url",
            "lp_off_url",
            "ext_temp_over_url",
            "ext_temp_under_url",
            "ext_hum_over_url",
            "ext_hum_under_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "default_state": "off",
            "btn_type": "toggle",
            "btn_reverse": 0,
            "auto_on": 0,
            "auto_off": 0,
            "power": 0,
            "schedule": false,
            "schedule_rules": [],
            "max_power": 0
        }
    ],
    "ext_sensors": {},
    "ext_temperature": {},
    "ext_humidity": {},
    "ext_switch_enable": 1,
    "ext_switch":{
      "0": {
        "relay_num": 0
      }
    }
}

```

[Common attributes](#settings) apply for the `/settings` endpoint. Additionally:

### Attributes ###

|          Attribute           |     Type      |                                                                                           Description                                                                                           |
|------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `factory_reset_from_switch`  |     bool      |                                                              Whether factory reset via 5-time flip of the input switch is enabled                                                               |
|         `max_power`          |    number     |                                                     **Shelly1PM only** Power threshold above which an overpower condition will be triggered                                                     |
|       `supply_voltage`       |    number     |                                                             **Shelly1PM only** Supply voltage of the device, 0 for 110V, 1 for 220V                                                             |
|      `power_correction`      |    number     |                                                                         **Shelly1PM only** Power correction coefficient                                                                         |
|            `mode`            |    string     |                                                                                         Always `relay`                                                                                          |
|     `led_status_disable`     |     bool      |                                                                   **Shelly1PM only** Whether LED status indication is enabled                                                                   |
|       `longpush_time`        |    number     |                                                                               Duration to detect long push, `ms`                                                                                |
|          `actions`           |     hash      |                                List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly1-1pm-settings-actions)                                 |
|           `relays`           |array of hashes|                                                        Current relay settings, see [`/settings/relay/0`](#shelly1-1pm-settings-relay-0)                                                         |
|`ext_sensors.temperature_unit`|    string     |                                                             **If add-on attached (DS1820/DHT22)**: External temperature unit `C/F`                                                              |
|      `ext_temperature`       |     hash      |           **If add-on attached (DS1820/DHT22)**: External temperature thresholds and actions, see [`/settings/ext_temperature/{index}`](#shelly1-1pm-settings-ext_temperature-index)            |
|        `ext_humidity`        |     hash      |                      **If add-on attached (DHT22 only)**: External humidity thresholds and actions, see [`/settings/ext_humidity/0`](#shelly1-1pm-settings-ext_humidity-0)                      |
|     `ext_switch_enable`      |    number     |                                                                           Whether low-power switch add-on is enabled                                                                            |
|         `ext_switch`         |     hash      |**If low-power switch add-on attached**: Information about the relay, which is controlled with the low-power switch, see [`/settings/ext_switch/{index}`](#shelly1-1pm-settings-ext_switch-index)|

[Common parameters](#settings) apply for the `/settings` endpoint. Additionally:

### Parameters ###

|          Parameter           | Type |                                      Description                                      |
|------------------------------|------|---------------------------------------------------------------------------------------|
| `factory_reset_from_switch`  | bool |           Enable/disable factory reset via 5-time flip of the input switch            |
|         `max_power`          |number|**Shelly1PM only** Power threshold above which an overpower condition will be triggered|
|       `supply_voltage`       |number|      **Shelly1PM only** Set supply voltage of the device, 0 for 110V, 1 for 220V      |
|          `actions`           | hash |     For setting actions, see [`/settings/actions`](#shelly1-1pm-settings-actions)     |
|      `power_correction`      |number|            **Shelly1PM only** Power correction coefficient, `[0.85-1.15]`             |
|            `mode`            |string|                        Only value `relay` is allowed for these                        |
|     `led_status_disable`     | bool |                   **Shelly1PM only** Disable LED status indication                    |
|       `longpush_time`        |number|                     Set duration to detect long push, `1..5000ms`                     |
|`ext_sensors_temperature_unit`|string|      **If add-on attached (DS1820/DHT22)**: Set external temperature unit `C/F`       |
|     `ext_switch_enable`      |number|                        Enable/disable low-power switch add-on                         |

Shelly1/1PM: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "lp_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "lp_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "ext_temp_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_temp_over_value": 24.0,
        "ext_temp_over_onetime": false
      }
    ],
    "ext_temp_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_temp_under_value": 22.5,
        "ext_temp_under_onetime": false
      }
    ],
    "ext_hum_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_hum_over_value": 60,
        "ext_hum_over_onetime": false
      }
    ],
    "ext_hum_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_hum_under_value": 40,
        "ext_hum_under_onetime": false
      }
    ]
  }
}

```

### Actions ###

Shelly1/1PM supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|       Action       |Index|                                                     Description                                                      |
|--------------------|-----|----------------------------------------------------------------------------------------------------------------------|
|    `btn_on_url`    |  0  |                                       URL to access when SW input is activated                                       |
|   `btn_off_url`    |  0  |                                      URL to access when SW input is deactivated                                      |
|    `out_on_url`    |  0  |                                        URL to access when output is activated                                        |
|   `out_off_url`    |  0  |                                       URL to access when output is deactivated                                       |
|   `longpush_url`   |  0  |URL to access on longpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`. |
|  `shortpush_url`   |  0  |URL to access on shortpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`.|
|    `lp_on_url`     |  0  |                  **If low-power switch add-on attached** URL to access when LP switch is activated                   |
|    `lp_off_url`    |  0  |                 **If low-power switch add-on attached** URL to access when LP switch is deactivated                  |
|`ext_temp_over_url` | 0-2 |              **If temperature add-on attached** URL to invoke when temperature \> `ext_temp_over_value`              |
|`ext_temp_under_url`| 0-2 |             **If temperature add-on attached** URL to invoke when temperature \< `ext_temp_under_value`              |
| `ext_hum_over_url` |  0  |         **If temperature add-on attached (DHT22 only)** URL to invoke when humidity \> `ext_hum_over_value`          |
|`ext_hum_under_url` |  0  |         **If temperature add-on attached (DHT22 only)** URL to invoke when humidity \< `ext_hum_under_value`         |

### Additional parameters ###

|       Parameter        | Type |                               Description                                |
|------------------------|------|--------------------------------------------------------------------------|
| `ext_temp_over_value`  |number|          Temperature over which to trigger `ext_temp_over_url`           |
|`ext_temp_over_onetime` | bool |Whether the `ext_temp_over_url` will be triggered repeatedly or only once |
| `ext_temp_under_value` |number|         Temperature under which to trigger `ext_temp_under_url`          |
|`ext_temp_under_onetime`| bool |Whether the `ext_temp_under_url` will be triggered repeatedly or only once|
|  `ext_hum_over_value`  |number|            Humidity over which to trigger `ext_hum_over_url`             |
| `ext_hum_over_onetime` | bool | Whether the `ext_hum_over_url` will be triggered repeatedly or only once |
| `ext_hum_under_value`  |number|           Humidity under which to trigger `ext_hum_under_url`            |
|`ext_hum_under_onetime` | bool |Whether the `ext_hum_under_url` will be triggered repeatedly or only once |

Shelly1/1PM: `/settings/relay/0`
----------

```
GET /settings/relay/0 (Shelly1PM)

{
    "name": null,
    "appliance_type": "General",
    "ison": false,
    "has_timer": false,
    "default_state": "off",
    "btn_type": "toggle",
    "btn_reverse": 0,
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": [],
    "max_power": 0
}

```

The returned document here is identical to the data returned in `/settings` for the single output channel in the `relays` array. The channel index exists to preserve API compatibility with multi-channel Shelly devices. Attributes in the response match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                                                           Description                                                            |
|----------------|----------------|----------------------------------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                                            Relay name                                                            |
|`appliance_type`|     string     |                                                Custom configurable appliance type                                                |
|     `ison`     |      bool      |                                                           Relay state                                                            |
|  `has_timer`   |      bool      |                                                 Whether there is an active timer                                                 |
|`default_state` |     string     |                                     State on power-on, one of `off`, `on`, `last`, `switch`                                      |
|   `btn_type`   |     string     |                 Button type, one of `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`                  |
| `btn_reverse`  |     number     |                                          Whether logical state of the input is inverted                                          |
|   `auto_on`    |     number     |                                                Automatic flip back timer, seconds                                                |
|   `auto_off`   |     number     |                                                Automatic flip back timer, seconds                                                |
|    `power`     |     number     |**Shelly1 only** User power constant to display in `meters` when relay is on, see [`/settings/power/0`](#shelly1-settings-power-0)|
|   `schedule`   |      bool      |                                                  Whether scheduling is enabled                                                   |
|`schedule_rules`|array of strings|                                                  Rules for schedule activation                                                   |
|  `max_power`   |     number     |                     **Shelly1PM only** power threshold above which an overpower condition will be triggered                      |

### Parameters ###

|   Parameter    |      Type      |                                                             Description                                                              |
|----------------|----------------|--------------------------------------------------------------------------------------------------------------------------------------|
|    `reset`     |      any       |                         Submitting a non-empty value will reset settings for the output to factory defaults                          |
|     `name`     |     string     |                                                            Set relay name                                                            |
|`appliance_type`|     string     |                                                Set custom configurable appliance type                                                |
|`default_state` |     string     |                                            Accepted values: `off`, `on`, `last`, `switch`                                            |
|   `btn_type`   |     string     |                     Accepted values: `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`                     |
| `btn_reverse`  |      bool      |                                                Inverts the logical state of the input                                                |
|   `auto_on`    |     number     |                            Automatic flip back timer, seconds. Will engage after turning Shelly1/1PM OFF                             |
|   `auto_off`   |     number     |                             Automatic flip back timer, seconds. Will engage after turning Shelly1/1PM ON                             |
|    `power`     |     number     |**Shelly1 only** Set user power constant to display in `meters` when relay is on, see [`/settings/power/0`](#shelly1-settings-power-0)|
|   `schedule`   |      bool      |                                                        Enable schedule timer                                                         |
|`schedule_rules`|array of strings|                                        Rules for schedule activation, e.g. `0000-0123456-on`                                         |
|  `max_power`   |     number     |                     **Shelly1PM only** Set power threshold above which an overpower condition will be triggered                      |

Shelly1: `/settings/power/0`
----------

### Parameters ###

|Parameter| Type |                                        Description                                         |
|---------|------|--------------------------------------------------------------------------------------------|
| `power` |number|**Shelly1 only** Set user power constant to display in `meters` when relay is on, `0..4000W`|

Shelly1/1PM: `/settings/ext_temperature/{index}`
----------

```
GET /settings/ext_temperature/0

{
    "overtemp_threshold_tC": 25.6,
    "overtemp_threshold_tF": 78.1,
    "undertemp_threshold_tC": 18.4,
    "undertemp_threshold_tF": 65.1,
    "overtemp_act": "disabled",
    "undertemp_act": "disabled",
    "offset_tC": 0,
    "offset_tF": 0
}

```

**Only applicable if add-on attached (DS1820/DHT22)**

### Parameters ###

|       Parameter        | Type |                            Description                             |
|------------------------|------|--------------------------------------------------------------------|
|`overtemp_threshold_tC` |number|      Temperature (in °C) over which to trigger `overtemp_act`      |
|`overtemp_threshold_tF` |number|      Temperature (in °F) over which to trigger `overtemp_act`      |
|`undertemp_threshold_tC`|number|     Temperature (in °C) under which to trigger `undertemp_act`     |
|`undertemp_threshold_tF`|number|     Temperature (in °F) under which to trigger `undertemp_act`     |
|     `overtemp_act`     |string|Over-temperature action, one of `disabled`, `relay_on`, `relay_off` |
|    `undertemp_act`     |string|Under-temperature action, one of `disabled`, `relay_on`, `relay_off`|
|      `offset_tC`       |number|                   Set temperature offset, in °C                    |
|      `offset_tF`       |number|                   Set temperature offset, in °F                    |

**Temperature thresholds:** The values of over-/under-temperature thresholds must be inside the ranges measurable by the DS1820/DHT22 sensors:

* DS1820: `[-55 / 125 ]°C`, `[-67 / 257]°F`
* DHT22: `[-40 / 80]°C`, `[-40 / 176]°F`

Shelly1/1PM: `/settings/ext_humidity/0`
----------

```
GET /settings/ext_humidity/0

{
    "overhum_threshold": 85.4,
    "underhum_threshold": 10.0,
    "overhum_act": "disabled",
    "underhum_act": "disabled",
    "offset": 0
}

```

**Only applicable if add-on attached (DHT22)**

### Parameters ###

|     Parameter      | Type |                           Description                           |
|--------------------|------|-----------------------------------------------------------------|
|`overhum_threshold` |number|       Humidity (in %) over which to trigger `overhum_act`       |
|`underhum_threshold`|number|      Humidity (in %) under which to trigger `underhum_act`      |
|   `overhum_act`    |string|Over-humidity action, one of `disabled`, `relay_on`, `relay_off` |
|   `underhum_act`   |string|Under-humidity action, one of `disabled`, `relay_on`, `relay_off`|
|      `offset`      |number|                    Set humidity offset, in %                    |

**Humidity thresholds:** The values of over-/under-humidity thresholds must be inside the range measurable by the DHT22 sensor: `[0/100]%`

Shelly1/1PM: `/settings/ext_switch/{index}`
----------

```
GET /settings/ext_switch/0

{
    "relay_num": 0
}

```

**Only applicable if low-power switch add-on attached**

### Parameters ###

| Parameter | Type |                                                Description                                                |
|-----------|------|-----------------------------------------------------------------------------------------------------------|
|`relay_num`|number|Relay number, which is controlled by the external switch. `-1` if no relay is controlled by the ext switch.|

Shelly1/1PM: `/status`
----------

```
GET /status (Shelly1PM without temperature add-on)

{
    "relays": [
        {
            "ison": false,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "source": "http"
        }
    ],
    "meters": [
        {
            "power": 0,
            "overpower": 23.78,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ],
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        }
    ],
    "ext_sensors": {},
    "ext_temperature": {},
    "ext_humidity": {},
    "temperature": 29.35,
    "overtemperature": false,
    "tmp": {
        "tC": 29.35,
        "tF": 84.83,
        "is_valid": true
    },
    "temperature_status":"Normal",
    "ext_switch":{
        "0": {
            "input": 1
        }
    }
}

```

`/status` is extended with information about the current state of the output channel as well as data from the power meter and external sensors (if available).

### Attributes ###

|          Attribute           |     Type      |                                                             Description                                                             |
|------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
|           `relays`           |array of hashes|    Contains the current state of the relay output channels. See [`/relay/0`](#shelly1-1pm-relay-0) for description of attributes    |
|           `meters`           |array of hashes|                 Contains information about instantaneous power and cumulative energy counter, see description below                 |
|           `inputs`           |array of hashes|                                         Current state of the inputs, see description below                                          |
|`ext_sensors.temperature_unit`|    string     |                               **If add-on attached (DS1820/DHT22)**: external temperature unit `C/F`                                |
|      `ext_temperature`       |     hash      |              **If add-on attached (DS1820/DHT22)**: external temperature data, see below for description of attributes              |
|        `ext_humidity`        |     hash      |                **If add-on attached (DHT22 only)**: external humidity data, see below for description of attributes                 |
|        `temperature`         |    number     |                                        **Shelly1PM only** internal device temperature in °C                                         |
|      `overtemperature`       |     bool      |                                        **Shelly1PM only** `true` when device has overheated                                         |
|           `tmp.tC`           |    number     |                                             **Shelly1PM only** Device temperature in °C                                             |
|           `tmp.tF`           |    number     |                                             **Shelly1PM only** Device temperature in °F                                             |
|        `tmp.is_valid`        |     bool      |                                       **Shelly1PM only** Whether device temperature is valid                                        |
|     `temperature_status`     |    string     |                        **Shelly1PM only** Temperature status of the device, "Normal", "High" or "Very High"                         |
|         `ext_switch`         |     hash      |**If low-power switch add-on attached**: Information about the status of the external switch, see below for description of attributes|

### `meters` attributes: Shelly1 ###

|Attribute | Type |                                                             Description                                                             |
|----------|------|-------------------------------------------------------------------------------------------------------------------------------------|
| `power`  |number|When relay is on, displays the value of the user power constant (see [`/settings/power/0`](#shelly1-settings-power-0)); otherwise `0`|
|`is_valid`| bool |                                                            Always `true`                                                            |

### `meters` attributes: Shelly1PM ###

**Note:** Energy counters (in the `counters` array and `total`) will reset to 0 after reboot.

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`overpower`|     number     |       Value in Watts, on which an overpower condition is detected       |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|    Energy counter value for the last 3 round minutes in Watt-minute     |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

### `inputs` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Input events are only detected when `btn_type` is configured as `momentary`, `momentary_on_release` or `detached`.

### `ext_temperature.{index}` attributes ###

### Attributes ###

|Attribute| Type |                         Description                         |
|---------|------|-------------------------------------------------------------|
| `hwID`  |string|               Hardware ID of sensor `{index}`               |
|  `tC`   |number|Temperature reading of sensor `{index}`, °C, `999` if invalid|
|  `tF`   |number|Temperature reading of sensor `{index}`, °F, `999` if invalid|

### `ext_humidity.0` attributes ###

### Attributes ###

|Attribute| Type |                      Description                      |
|---------|------|-------------------------------------------------------|
| `hwID`  |string|                Hardware ID of sensor 0                |
|  `hum`  |number|Humidity reading of sensor 0, percent, `999` if invalid|

### `ext_switch.{index}` attributes ###

**Only applicable if low-power switch add-on attached**

### Attributes ###

|Parameter| Type |        Description         |
|---------|------|----------------------------|
| `input` |number|State of the external switch|

Shelly1/1PM: `/relay/0`
----------

```
GET /relay/0 (Shelly1PM)

{
    "ison": false,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "source": "http"
}

```

Shows current status of the output channel and accepts commands for controlling the channel.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                   **Shelly1PM only** if maximum allowed power was exceeded                   |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly1: flash/debug, power options
----------

Shelly1 comes with a programming/debug header which can be used to flash alternative firmwares on the device. It has an ESP8266 inside, with a 2MB flash chip. A USB-to-UART adapter is needed as well as a reliable 3.3V source with at least 350 mA drive capability. The following diagram shows the device pinout and power source voltage selection jumper:

The flash/debug connetor should **never** be used while the device is connected to the grid or another power supply. When connecting to a PC, please provide a reliable 3.3V source externally.

To boot the ESP8266 for serial programming, tie `GPIO0` to `GND` before powering up. Flashing can be done with [`esptool`](https://github.com/espressif/esptool). There is a very wide range of platforms, languages and libraries for the ESP8266 chip which can be used to integrate the device with virtually any system. A few examples are:

* [Espressif's SDK](https://www.espressif.com/en/support/download/sdks-demos)
* [Arduino](https://github.com/esp8266/Arduino)
* [NodeMCU](http://nodemcu.com/)
* [Micropython](https://docs.micropython.org/en/latest/esp8266/esp8266/tutorial/intro.html)
* [Sming](https://github.com/SmingHub/Sming)
* and many others.

Shelly1: wiring in the field
----------

When using DC power supply, observe polarity as indicated:

**Note:** Internally, `GND` from the flash/debug connector is connected to the `AC/L` terminal. `SW` can be wired through a switch to either `L` or `N` and will detect transitions between open and closed state of the switch.

Shelly1L
==========

Shelly1L: Overview
----------

Shelly1L is the smallest intelligent Wi-Fi power switch on the market today. Visit the product page for detailed description and User Manual:

<https://shop.shelly.cloud/shelly-1l-wifi-smart-home-automation>

Commands to turn the relay on or off can come from:

* A physical button
* HTTP request, trough the local web interface
* A command sent via the cloud or MQTT
* A weekly-schedule event or a sunrise/sunset-generated event
* Overpower condition will turn the relay OFF

Shelly 1L supports up to 18 schedule rules.

### Factory Reset ###

If the web interface of the device cannot be accessed, settings can be brought back to default by switching ON and OFF 5 times the physical switch connected to the device, within the first minute after a reboot or power-on.

### About the device ###

Shelly1L supports the **ON** and **OFF** commands which control the coil of a 4.1A 250VAC relay.

Shelly1L also supports `auto_on` and `auto_off` settings -- these are timers in seconds which will turn the device ON or OFF when it has been turned OFF or ON respectively, from either a physical button or network command. Thus, the user can set a limit for how long the device can be **ON** or **OFF**.

Upon power-on, output is initialized using one of 4 available strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly

To control Shelly1L, use these resources:

* [`/settings/relay/0`](#shelly1l-settings-relay-0) to configure behavior
* [`/relay/0`](#shelly1l-relay-0) to control and monitor

Shelly1L: MQTT
----------

Shelly1L uses the following topics:

* `shellies/shelly1l-<deviceid>/relay/0` to report status: `on`, `off` or `overpower` (the latter only for Shelly1L)
* `shellies/shelly1l-<deviceid>/relay/0/command` accepts `on`, `off` or `toggle` and applies accordingly
* `shellies/shelly1l-<deviceid>/input/0` reports the state of the `SW` terminal
* `shellies/shelly1l-<deviceid>/longpush/0` reports `longpush` state as `0` (shortpush) or `1` (longpush)
* `shellies/shelly1l-<deviceid>/input_event/0` reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly1l-status) for details

* `shellies/shelly1l-<deviceid>/relay/0/power` reports instantaneous power in Watts

* `shellies/shelly1l-<deviceid>/relay/0/energy` reports an incrementing energy counter in Watt-minute

* `shellies/shelly1l-<deviceid>/temperature` reports internal device temperature in °C

* `shellies/shelly1l-<deviceid>/temperature_f` reports internal device temperature in °F

* `shellies/shelly1l-<deviceid>/overtemperature` reports `1` when device has overheated, normally `0`

* `shellies/shelly1l-<deviceid>/relay/0/overpower_value` reports the value in Watts, on which an overpower condition is detected

Shelly1L: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly 1L SHSW-L](docs/coiot/v2/examples/Shelly%201L%20SHSW-L%20no-addon)

Shelly1L: `/settings`
----------

```
GET /settings

{
    "factory_reset_from_switch": true,
    "max_power": 2000,
    "supply_voltage": 0,
    "mode": "relay",
    "led_status_disable": false,
    "longpush_time": 1000,
    "actions": {
        "active": false,
        "names": [
            "btn1_on_url",
            "btn1_off_url",
            "btn1_longpush_url",
            "btn1_shortpush_url",
            "btn2_on_url",
            "btn2_off_url",
            "btn2_longpush_url",
            "btn2_shortpush_url",
            "out_on_url",
            "out_off_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "default_state": "off",
            "btn1_type": "toggle",
            "btn1_reverse": 0,
            "btn2_type": "toggle",
            "btn2_reverse": 0,
            "swap_inputs": false,
            "auto_on": 0,
            "auto_off": 0,
            "power": 0,
            "schedule": false,
            "schedule_rules": [],
            "max_power": 0
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ]
}

```

[Common attributes](#settings) apply for the `/settings` endpoint. Additionally:

### Attributes ###

|         Attribute         |     Type      |                                                         Description                                                         |
|---------------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|     bool      |                            Whether factory reset via 5-time flip of the input switch is enabled                             |
|        `max_power`        |    number     |                            Power threshold above which an overpower condition will be triggered                             |
|     `supply_voltage`      |    number     |                                    Supply voltage of the device, 0 for 110V, 1 for 220V                                     |
|          `mode`           |    string     |                                                       Always `relay`                                                        |
|   `led_status_disable`    |     bool      |                                          Whether LED status indication is enabled                                           |
|      `longpush_time`      |    number     |                                             Duration to detect long push, `ms`                                              |
|         `actions`         |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly1l-settings-actions)|
|         `relays`          |array of hashes|                        Current relay settings, see [`/settings/relay/0`](#shelly1l-settings-relay-0)                        |
|         `meters`          |array of hashes|       Contains information about instantaneous power and cumulative energy counter, see [`/status`](#shelly1l-status)       |

[Common parameters](#settings) apply for the `/settings` endpoint. Additionally:

### Parameters ###

|         Parameter         | Type |                               Description                                |
|---------------------------|------|--------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |     Enable/disable factory reset via 5-time flip of the input switch     |
|        `max_power`        |number|   Power threshold above which an overpower condition will be triggered   |
|     `supply_voltage`      |number|         Set supply voltage of the device, 0 for 110V, 1 for 220V         |
|         `actions`         | hash |For setting actions, see [`/settings/actions`](#shelly1l-settings-actions)|
|          `mode`           |string|                 Only value `relay` is allowed for these                  |
|   `led_status_disable`    | bool |                      Disable LED status indication                       |
|      `longpush_time`      |number|              Set duration to detect long push, `1..5000ms`               |

Shelly1L: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn1_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn1_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn1_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn1_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly1L supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|       Action       |Index|                                                     Description                                                      |
|--------------------|-----|----------------------------------------------------------------------------------------------------------------------|
|   `btn1_on_url`    |  0  |                                       URL to access when SW input is activated                                       |
|   `btn1_off_url`   |  0  |                                      URL to access when SW input is deactivated                                      |
|`btn1_longpush_url` |  0  |URL to access on longpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`. |
|`btn1_shortpush_url`|  0  |URL to access on shortpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`.|
|   `btn2_on_url`    |  0  |                                       URL to access when SW input is activated                                       |
|   `btn2_off_url`   |  0  |                                      URL to access when SW input is deactivated                                      |
|`btn2_longpush_url` |  0  |URL to access on longpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`. |
|`btn2_shortpush_url`|  0  |URL to access on shortpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`.|
|    `out_on_url`    |  0  |                                        URL to access when output is activated                                        |
|   `out_off_url`    |  0  |                                       URL to access when output is deactivated                                       |

Shelly1L: `/settings/relay/0`
----------

```
GET /settings/relay/0 (Shelly1L)

{
    "name": null,
    "appliance_type": "General",
    "ison": false,
    "has_timer": false,
    "default_state": "off",
    "btn1_type": "toggle",
    "btn1_reverse": 0,
    "btn2_type": "toggle",
    "btn2_reverse": 0,
    "swap_inputs": false,
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": [],
    "max_power": 0
}

```

The returned document here is identical to the data returned in `/settings` for the single output channel in the `relays` array. The channel index exists to preserve API compatibility with multi-channel Shelly devices. Attributes in the response match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                                                                                               Description                                                                                                |
|----------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                                                                                Relay name                                                                                                |
|`appliance_type`|     string     |                                                                                    Custom configurable appliance type                                                                                    |
|     `ison`     |      bool      |                                                                                               Relay state                                                                                                |
|  `has_timer`   |      bool      |                                                                                     Whether there is an active timer                                                                                     |
|`default_state` |     string     |                                                                   State on power-on, one of `off`, `on`, `last`, `switch1`, `switch2`                                                                    |
|  `btn1_type`   |     string     |Button type, one of `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`, `dual_momentary`, `dual_toggle`, `dual_edge`, `dual_detached`, `dual_action`, `dual_momentary_on_release`|
| `btn1_reverse` |     number     |                                                                              Whether logical state of the input is inverted                                                                              |
|  `btn2_type`   |     string     |Button type, one of `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`, `dual_momentary`, `dual_toggle`, `dual_edge`, `dual_detached`, `dual_action`, `dual_momentary_on_release`|
| `btn2_reverse` |     number     |                                                                              Whether logical state of the input is inverted                                                                              |
| `swap_inputs`  |      bool      |                                                                                        Whether inputs are swapped                                                                                        |
|   `auto_on`    |     number     |                                                                                    Automatic flip back timer, seconds                                                                                    |
|   `auto_off`   |     number     |                                                                                    Automatic flip back timer, seconds                                                                                    |
|    `power`     |     number     |                                            User power constant to display in `meters` when relay is on, see [`/settings/power/0`](#shelly1-settings-power-0)                                             |
|   `schedule`   |      bool      |                                                                                      Whether scheduling is enabled                                                                                       |
|`schedule_rules`|array of strings|                                                                                      Rules for schedule activation                                                                                       |
|  `max_power`   |     number     |                                                                   power threshold above which an overpower condition will be triggered                                                                   |

### Parameters ###

|   Parameter    |      Type      |                                                                                              Description                                                                                              |
|----------------|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `reset`     |      any       |                                                          Submitting a non-empty value will reset settings for the output to factory defaults                                                          |
|     `name`     |     string     |                                                                                            Set relay name                                                                                             |
|`appliance_type`|     string     |                                                                                Set custom configurable appliance type                                                                                 |
|`default_state` |     string     |                                                                      Accepted values: `off`, `on`, `last`, `switch1`, `switch2`                                                                       |
|  `btn1_type`   |     string     |Accepted values: `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`, `dual_momentary`, `dual_toggle`, `dual_edge`, `dual_detached`, `dual_action`, `dual_momentary_on_release`|
| `btn1_reverse` |      bool      |                                                                                Inverts the logical state of the input                                                                                 |
|  `btn2_type`   |     string     |Accepted values: `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`, `dual_momentary`, `dual_toggle`, `dual_edge`, `dual_detached`, `dual_action`, `dual_momentary_on_release`|
| `btn2_reverse` |      bool      |                                                                                Inverts the logical state of the input                                                                                 |
| `swap_inputs`  |      bool      |                                                                                      Whether inputs are swapped                                                                                       |
|   `auto_on`    |     number     |                                                              Automatic flip back timer, seconds. Will engage after turning Shelly1L OFF                                                               |
|   `auto_off`   |     number     |                                                               Automatic flip back timer, seconds. Will engage after turning Shelly1L ON                                                               |
|    `power`     |     number     |                                         Set user power constant to display in `meters` when relay is on, see [`/settings/power/0`](#shelly1-settings-power-0)                                         |
|   `schedule`   |      bool      |                                                                                         Enable schedule timer                                                                                         |
|`schedule_rules`|array of strings|                                                                         Rules for schedule activation, e.g. `0000-0123456-on`                                                                         |
|  `max_power`   |     number     |                                                               Set power threshold above which an overpower condition will be triggered                                                                |

Shelly1L: `/settings/power/0`
----------

### Parameters ###

|Parameter| Type |                                Description                                |
|---------|------|---------------------------------------------------------------------------|
| `power` |number|Set user power constant to display in `meters` when relay is on, `0..4000W`|

Shelly1L: `/status`
----------

```
GET /status

{
    "relays": [
        {
            "ison": false,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "source": "http"
        }
    ],
    "meters": [
        {
            "power": 0,
            "overpower": 23.78,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ],
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        },
        {
            "input": 1,
            "event": "S",
            "event_cnt": 2
        }
    ],
    "temperature": 29.35,
    "overtemperature": false,
    "tmp": {
        "tC": 29.35,
        "tF": 84.83,
        "is_valid": true
    },
    "temperature_status":"Normal"
}

```

`/status` is extended with information about the current state of the output channel as well as data from the power meter.

### Attributes ###

|     Attribute      |     Type      |                                                       Description                                                        |
|--------------------|---------------|--------------------------------------------------------------------------------------------------------------------------|
|      `relays`      |array of hashes|Contains the current state of the relay output channels. See [`/relay/0`](#shelly1l-relay-0) for description of attributes|
|      `meters`      |array of hashes|           Contains information about instantaneous power and cumulative energy counter, see description below            |
|      `inputs`      |array of hashes|                                    Current state of the inputs, see description below                                    |
|   `temperature`    |    number     |                                            internal device temperature in °C                                             |
| `overtemperature`  |     bool      |                                            `true` when device has overheated                                             |
|      `tmp.tC`      |    number     |                                                 Device temperature in °C                                                 |
|      `tmp.tF`      |    number     |                                                 Device temperature in °F                                                 |
|   `tmp.is_valid`   |     bool      |                                           Whether device temperature is valid                                            |
|`temperature_status`|    string     |                            Temperature status of the device, "Normal", "High" or "Very High"                             |

### `meters` attributes: Shelly1L ###

**Note:** Energy counters (in the `counters` array and `total`) will reset to 0 after reboot.

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`overpower`|     number     |       Value in Watts, on which an overpower condition is detected       |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|    Energy counter value for the last 3 round minutes in Watt-minute     |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

### `inputs` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Input events are only detected when `btn_type` is configured as `momentary`, `momentary_on_release` or `detached`.

Shelly1L: `/relay/0`
----------

```
GET /relay/0 (Shelly1L)

{
    "ison": false,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "source": "http"
}

```

Shows current status of the output channel and accepts commands for controlling the channel.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                            if maximum allowed power was exceeded                             |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly1L: wiring in the field
----------

When using DC power supply, observe polarity as indicated:

**Note:** Internally, `GND` from the flash/debug connector is connected to the `AC/L` terminal. `SW` can be wired through a switch to either `L` or `N` and will detect transitions between open and closed state of the switch.

Shelly2
==========

Shelly2: Overview
----------

Shelly2 is a WiFi-enabled dual-channel relay with a common power meter.

Shelly2 can operate in two distinct device modes: **Relay** and**Roller Shutter**. Devices are initially programmed to work in **Relay** mode. The operating mode of Shelly2 can be set via the [`/settings`](#shelly2-settings) endpoint. Commands to perform actions can come from:

* A physical input switch (S1/S2)
* HTTP request, trough the local web interface
* A command sent via the cloud
* A weekly-schedule event or a sunrise/sunset-generated event

Shelly2 supports up to 20 schedule rules.

### Factory Reset ###

If the web interface of the device cannot be accessed, settings can be brought back to default by switching ON and OFF 5 times the physical switch connected to the device, within the first minute after a reboot or power-on.

Shelly2 in Relay Mode
----------

In **Relay** mode, each of the two channels is controlled individually and supports the **ON** and **OFF** commands. In this mode, an overpower threshold can be enabled for each of the two channels, via the `max_power` parameter in [`/settings`](#shelly2-settings). If set to a value different than 0, the relay will automatically turn off if current power consumption exceeds:

* the value of `max_power` when only one channel is **ON**
* twice the value of `max_power` when both channels are **ON**

Relay channels also support `auto_on` and `auto_off` settings -- these are timers in seconds which will turn ON or OFF the channel when it has been turned OFF or ON respectively, from either a physical switch or network command. Thus, the user can set a limit for how long the channel can be **ON** or **OFF**.

Upon power-on, outputs are initialized using one of 4 available strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly

Physical input switches can be one of:

* a momentary, push-button switch
* a toggle switch with two stable states
* an "edge" switch. In this input mode, every switch state transition causes a toggle of the output state. This can be used with input from existing two-way switch installations
* detached, inputs do not control the relays

**Note:** Setting output state based on inputs on power-on is not supported when inputs are configured as momentary or edge.

To control Shelly2 in **Relay** mode, use these resources:

* [`/settings/relay/{index}`](#shelly2-settings-relay-index) to configure the behavior of each channel
* [`/relay/{index}`](#shelly2-relay-index) to control and monitor the channel

Shelly2 in Roller Mode
----------

In **Roller** mode the device can be used to control a bi-directional motor, with optional obstacle detection and safety switch features. Commands are: **Open**, **Close** and **Stop**.

Shelly2 has a single logical **Roller**, but we index the HTTP resources to allow for future devices with more output channels and **Roller**-s.

When Shelly2 is in **Roller** mode, use:

* [`/settings/roller/{index}`](#shelly2-settings-roller-index) to configure the behavior of this **Roller** controller, including the advanced features described below
* [`/roller/{index}`](#shelly2-roller-index) to query the state and send commands

### Obstacle detection ###

In **Roller** mode, the integrated power meter of Shelly2 can be used to detect motor overload which usually means something obstructing the movement of the door or roller shutter. A set of parameters define the behavior of Shelly2 when such event occurs. These are:

* the direction of motion for which obstacle protection is enabled
* the action to perform when the event occurs
* number of seconds to wait before triggering the condition -- motors draw big initial current which may be falsely interpreted as an obstacle

### Safety-switch input ###

While in **Roller** Mode and when inputs are configured as `onebutton`, the second physical input can be used as a safety input -- it can be tied to an end-stop switch or user safety stop button. Its configuration parameters are:

* when to honor events on the safety input: during either direction or any direction of motion
* what to do when the switch is engaged:
  * stop the motion
  * pause the motion, so when the switch is disengaged it continues in the same direction

* which external commands are allowed while the safety inputs is engaged

Shelly2: MQTT
----------

Shelly2 allows control and monitoring over MQTT for both relay and roller modes. Device mode, along with other parameters need to be configured using the mobile application or web interface. In either mode, Shelly2 reports:

* `shellies/shellyswitch-<deviceid>/input/<i>` for each SW input `<i>`; reports the current state as `0` or `1`
* `shellies/shellyswitch25-<deviceid>/voltage` reports the device voltage, in [V](ex.%20`230.00`)

### MQTT in Relay mode ###

Input events can be monitored on:

* `shellies/shellyswitch-<deviceid>/longpush/<i>` for each SW input `<i>`; reports a value indicating longpush state as `0` (shortpush) or `1` (longpush)
* `shellies/shellyswitch-<deviceid>/input_event/<i>` for each SW input `<i>`; reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly2-status) for details

In relay mode, the following topics can be used to read and set output channels `0` and `1`:

* `shellies/shellyswitch-<deviceid>/relay/<i>` to report status: `on`, `off` or `overpower`
* `shellies/shellyswitch-<deviceid>/relay/<i>/command` accepts `on`, `off` or `toggle`

The device measures the total consumption on both channels, which can be seen on:

* `shellies/shellyswitch-<deviceid>/relay/power` reports instantaneous power consumption rate in Watts
* `shellies/shellyswitch-<deviceid>/relay/energy` reports amount of energy consumed in Watt-minute
* `shellies/shellyswitch-<deviceid>/relay/<i>/overpower_value` for each relay `<i>` reports the value in Watts, on which an overpower condition is detected

### MQTT in Roller mode ###

When configured to operate in roller mode, MQTT topics used by Shelly2 are:

* `shellies/shellyswitch-<deviceid>/roller/0` reports the current state: `open` or `close` while in motion, `stop` when not moving.
* `shellies/shellyswitch-<deviceid>/roller/0/command` accepts `rc` (performs roller calibration), `open`, `close` and `stop`.

The device measures the consumption, which can be seen on:

* `shellies/shellyswitch-<deviceid>/roller/0/power` reports instantaneous power consumption rate in Watts
* `shellies/shellyswitch-<deviceid>/roller/0/energy` reports amount of energy consumed in Watt-minute

Since v1.4.0: roller mode position control. For this to work, the device must first be successfully calibrated, so that the time it takes for closing and opening are known.

* `shellies/shellyswitch-<deviceid>/roller/0/pos` reports the current position in percent, `-1` if invalid
* `shellies/shellyswitch-<deviceid>/roller/0/command/pos` accepts a number between 0 and 100, which is the target position in percent

Shelly2: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly 2 SHSW-21 relay-mode](docs/coiot/v2/examples/Shelly%202%20SHSW-21%20relay-mode)
* [Shelly 2 SHSW-21 roller-mode](docs/coiot/v2/examples/Shelly%202%20SHSW-21%20roller-mode)

Shelly2: `/settings`
----------

```
GET /settings

{
    "factory_reset_from_switch": true,
    "mode": "relay",
    "max_power": 1840,
    "longpush_time": 1000,
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "btn_off_url",
            "out_on_url",
            "out_off_url",
            "longpush_url",
            "shortpush_url",
            "roller_open_url",
            "roller_close_url",
            "roller_stop_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "switch",
            "btn_type": "toggle",
            "btn_reverse": 0,
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        },
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "switch",
            "btn_type": "toggle",
            "btn_reverse": 0,
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        }
    ],
    "rollers": [
        {
            "maxtime": 20,
            "maxtime_open": 20,
            "maxtime_close": 20,
            "default_state": "stop",
            "swap": false,
            "swap_inputs": false,
            "input_mode": "openclose",
            "button_type": "toggle",
            "btn_reverse": 0,
            "state": "stop",
            "power": 0,
            "is_valid": false,
            "safety_switch": false,
            "schedule": false,
            "schedule_rules": [],
            "obstacle_mode": "disabled",
            "obstacle_action": "stop",
            "obstacle_power": 200,
            "obstacle_delay": 1,
            "safety_mode": "while_opening",
            "safety_action": "stop",
            "safety_allowed_on_trigger": "none",
            "off_power": 2,
            "positioning": true
        }
    ]
}

```

Shelly2 extends the common `/settings` endpoint with relay and roller-mode specific data, power consumption status and contains the settings for this device's **Relays** and **Rollers** and adds [`/settings/relay/{index}`](#shelly2-settings-relay-index) and [`/settings/roller/{index}`](#shelly2-settings-roller-index) for setting the parameters.

### Attributes ###

|         Attribute         |     Type      |                                                        Description                                                         |
|---------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|     bool      |                            Whether factory reset via 5-time flip of an input switch is enabled                             |
|          `mode`           |    string     |                                                    `relay` or `roller`                                                     |
|        `max_power`        |    number     |                                                Overpower threshold in Watts                                                |
|      `longpush_time`      |    number     |                                             Duration to detect long push, `ms`                                             |
|         `actions`         |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly2-settings-actions)|
|         `relays`          |array of hashes|                  See [`/settings/relay/{index}`](#shelly2-settings-relay-index) for explanation of values                  |
|         `rollers`         |array of hashes|                 See [`/settings/roller/{index}`](#shelly2-settings-roller-index) for explanation of values                 |

### Parameters ###

|         Parameter         | Type |                               Description                               |
|---------------------------|------|-------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |     Enable/disable factory reset via 5-time flip of an input switch     |
|          `mode`           |string|                Accepted values are `relay` and `roller`                 |
|        `max_power`        |number|                      Overpower threshold in Watts                       |
|         `actions`         | hash |For setting actions, see [`/settings/actions`](#shelly2-settings-actions)|
|      `longpush_time`      |number|              Set duration to detect long push, `1..5000ms`              |

Shelly2: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "roller_open_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "roller_close_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "roller_stop_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly2 supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action      |Index|                                                     Description                                                      |
|------------------|-----|----------------------------------------------------------------------------------------------------------------------|
|   `btn_on_url`   | 0-1 |                                       URL to access when SW input is activated                                       |
|  `btn_off_url`   | 0-1 |                                      URL to access when SW input is deactivated                                      |
|   `out_on_url`   | 0-1 |                                        URL to access when output is activated                                        |
|  `out_off_url`   | 0-1 |                                       URL to access when output is deactivated                                       |
|  `longpush_url`  | 0-1 |URL to access on longpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`. |
| `shortpush_url`  | 0-1 |URL to access on shortpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`.|
|`roller_open_url` |  0  |                                          URL to access when roller is open                                           |
|`roller_close_url`|  0  |                                         URL to access when roller is closed                                          |
|`roller_stop_url` |  0  |                                         URL to access when roller is stopped                                         |

Shelly2: `/settings/relay/{index}`
----------

```
GET /settings/relay/0

{
    "name": null,
    "appliance_type": "General",
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "btn_type": "toggle",
    "btn_reverse": 0,
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": []
}

```

The returned document here is identical to the data returned in `/settings` for the particular output channel in the `relays` array. The attributes match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                                              Description                                               |
|----------------|----------------|--------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                               Relay name                                               |
|`appliance_type`|     string     |                                   Custom configurable appliance type                                   |
|     `ison`     |      bool      |                                             Channel state                                              |
|  `has_timer`   |      bool      |                            Whether there is an active timer on the channel                             |
|  `overpower`   |      bool      |                              Whether an overpower condition has occurred                               |
|`default_state` |     string     |                      Default power-on state, one of `off`, `on`, `last`, `switch`                      |
|   `btn_type`   |     string     |Button type, one of `momentary`, `toggle`, `edge`, `detached`, `action`, `cycle`, `momentary_on_release`|
| `btn_reverse`  |     number     |                                 Whether input switch state is inverted                                 |
|   `auto_on`    |     number     |             Automatic flip back timer, seconds. Will engage after turning the channel OFF              |
|   `auto_off`   |     number     |              Automatic flip back timer, seconds. Will engage after turning the channel ON              |
|   `schedule`   |      bool      |                                     Whether scheduling is enabled                                      |
|`schedule_rules`|array of strings|                                     Rules for schedule activation                                      |

### Parameters ###

|   Parameter    |      Type      |                                           Description                                            |
|----------------|----------------|--------------------------------------------------------------------------------------------------|
|    `reset`     |      any       |Submitting a non-empty value will reset settings for this relay output channel to factory defaults|
|     `name`     |     string     |                                            Relay name                                            |
|`appliance_type`|     string     |                              Set custom configurable appliance type                              |
|`default_state` |     string     |                          Accepted values: `off`, `on`, `last`, `switch`                          |
|   `btn_type`   |     string     |   Accepted values: `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`   |
| `btn_reverse`  |      bool      |                              Inverts the logical state of the input                              |
|   `auto_on`    |     number     |          Automatic flip back timer, seconds. Will engage after turning the channel OFF           |
|   `auto_off`   |     number     |           Automatic flip back timer, seconds. Will engage after turning the channel ON           |
|   `schedule`   |      bool      |                                      Enable schedule timer                                       |
|`schedule_rules`|array of strings|                      Rules for schedule activation, e.g. `0000-0123456-on`                       |

Shelly2: `/settings/roller/{index}`
----------

```
GET /settings/roller/0

{
    "maxtime": 20,
    "maxtime_open": 0,
    "maxtime_close": 0,
    "default_state": "stop",
    "swap": false,
    "swap_inputs": false,
    "input_mode": "onebutton",
    "button_type": "toggle",
    "btn_reverse": 0,
    "state": "stop",
    "power": 0,
    "is_valid": true,
    "safety_switch": false,
    "schedule": false,
    "schedule_rules": [],
    "obstacle_mode": "disabled",
    "obstacle_action": "stop",
    "obstacle_power": 200,
    "obstacle_delay": 1,
    "safety_mode": "while_opening",
    "safety_action": "stop",
    "safety_allowed_on_trigger": "none",
    "off_power": 0,
    "positioning": false
}

```

The returned document here is identical to the data returned in `/settings` as a hash in the `rollers`. The attributes match the set of accepted parameters.

### Attributes ###

|         Attribute         |      Type      |                                                                       Description                                                                        |
|---------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|         `maxtime`         |     number     |                                      The maximum time needed for the mechanism to completely open or close, seconds                                      |
|      `maxtime_open`       |     number     |                                          The maximum time needed for the mechanism to completely open, seconds                                           |
|      `maxtime_close`      |     number     |                                          The maximum time needed for the mechanism to completely close, seconds                                          |
|      `default_state`      |     string     |                                   One of `stop`, `open`, `close`. This parameters determines the behavior on power-on                                    |
|          `swap`           |      bool      |                                                        Whether to swap OPEN and CLOSE directions                                                         |
|       `swap_inputs`       |      bool      |                                                                Whether inputs are swapped                                                                |
|       `input_mode`        |     string     |One of `openclose` -- each input controls one direction of motion, `onebutton` -- a single button press cycles through states: open, stop, close, stop ...|
|       `button_type`       |     string     |                                                   One of `momentary`, `toggle`, `detached` or `action`                                                   |
|       `btn_reverse`       |     number     |                                            Whether to invert the state of input switch before interpreting it                                            |
|          `state`          |      bool      |                                                              One of `stop`, `open`, `close`                                                              |
|          `power`          |     number     |                                                            Current power consumption in Watts                                                            |
|        `is_valid`         |      bool      |                                                          If the power meter functions properly                                                           |
|      `safety_switch`      |      bool      |                                                     Whether the safety input is currently triggered                                                      |
|        `schedule`         |      bool      |                                                              Whether scheduling is enabled                                                               |
|     `schedule_rules`      |array of strings|                                                              Rules for schedule activation                                                               |
|      `obstacle_mode`      |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|     `obstacle_action`     |     string     |                                                                 One of `stop`, `reverse`                                                                 |
|     `obstacle_power`      |     number     |                                               Power threshold for triggering `"obstacle"` condition, Watts                                               |
|     `obstacle_delay`      |     number     |                               Number of seconds to wait after powering on the motor before obstacle detection is activated                               |
|       `safety_mode`       |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|      `safety_action`      |     string     |                                                            One of `stop`, `pause`, `reverse`                                                             |
|`safety_allowed_on_trigger`|     string     |                             Which commands are allowed while the safety switch is triggered: `none`, `open`, `close`, `all`                              |
|        `off_power`        |     number     |                      Power value below which the roller is considered "stopped", i.e. the actuator is stopped by an end-stop switch                      |
|       `positioning`       |      bool      |                                                 Whether the device is calibrated for positioning control                                                 |

### Parameters ###

|         Parameter         |      Type      |                                                                       Description                                                                        |
|---------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|          `reset`          |      any       |                                     Submitting a non-empty value will reset **Roller** settings to factory defaults                                      |
|         `maxtime`         |     number     |                                      The maximum time needed for the mechanism to completely open or close, seconds                                      |
|      `maxtime_open`       |     number     |                                          The maximum time needed for the mechanism to completely open, seconds                                           |
|      `maxtime_close`      |     number     |                                          The maximum time needed for the mechanism to completely close, seconds                                          |
|      `default_state`      |     string     |                                    One of `stop`, `open`, `close`. This parameter determines the behavior on power-on                                    |
|          `swap`           |      bool      |                                                        Whether to swap OPEN and CLOSE directions                                                         |
|       `swap_inputs`       |      bool      |                                                                  Whether to swap inputs                                                                  |
|       `input_mode`        |     string     |One of `openclose` -- each input controls one direction of motion, `onebutton` -- a single button press cycles through states: open, stop, close, stop ...|
|        `btn_type`         |     string     |                                                   One of `momentary`, `toggle`, `detached` or `action`                                                   |
|       `btn_reverse`       |      bool      |                                                          Inverts the logical state of the input                                                          |
|        `schedule`         |      bool      |                                                                  Enable schedule timer                                                                   |
|     `schedule_rules`      |array of strings|                                                  Rules for schedule activation, e.g. `0000-0123456-on`                                                   |
|      `obstacle_mode`      |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|     `obstacle_action`     |     string     |                                                                One of `stop`, `reverse`.                                                                 |
|        `off_power`        |     number     |                      Power value below which the roller is considered "stopped", i.e. the actuator is stopped by an end-stop switch                      |
|       `positioning`       |      bool      |                                                               Positioning enabled/disabled                                                               |
|     `obstacle_power`      |     number     |                                                Power threshold for triggering "obstacle" condition, Watts                                                |
|     `obstacle_delay`      |     number     |                               Number of seconds to wait after powering on the motor before obstacle detection is activated                               |
|       `safety_mode`       |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|      `safety_action`      |     string     |                                                            One of `stop`, `pause`, `reverse`                                                             |
|`safety_allowed_on_trigger`|     string     |                             Which commands are allowed while the safety switch is triggered: `none`, `open`, `close`, `all`                              |

Shelly2: `/status`
----------

```
GET /status (in relay mode)

"relays": [
    {
        "ison": false,
        "has_timer": false,
        "timer_started": 0,
        "timer_duration": 0,
        "timer_remaining": 0,
        "overpower": false,
        "is_valid": true,
        "source": "http"
    },
    {
        "ison": false,
        "has_timer": false,
        "timer_started": 0,
        "timer_duration": 0,
        "timer_remaining": 0,
        "overpower": false,
        "is_valid": true,
        "source": "cloud"
    }
],
"meters": [
    {
        "power": 0,
        "overpower": 23.78,
        "is_valid": true,
        "timestamp": 0,
        "counters": [1,2,3],
        "total": 4
    }
],
"inputs": [
    {
        "input": 0,
        "event": "S",
        "event_cnt": 2
    },
    {
        "input": 0,
        "event": "S",
        "event_cnt": 2
    }
]

```

Shelly2 adds information about the current state of the output channels, the logical `roller` device and power metering.

### Attributes ###

|Attribute|     Type      |                                                                             Description                                                                             |
|---------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`relays` |array of hashes|  Displayed in **Relay** mode: Contains the current state of the relay output channels. See [`/relay/{index}`](#shelly2-relay-index) for description of attributes   |
|`rollers`|array of hashes|Displayed in **Roller** mode: Contains the current state of the logical `roller` device. See [`/roller/{index}`](#shelly2-roller-index) for description of attributes|
|`meters` |array of hashes|                                                      Current status of the power meters, see description below                                                      |
|`inputs` |array of hashes|                                                         Current state of the inputs, see description below                                                          |

### `inputs.{index}` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Input events are only detected in `relay` mode and only when `btn_type` is configured as `momentary`, `momentary_on_release` or `detached`.

Shelly2: `/meter/{index}`
----------

```
GET /meter/0

{
    "power": 0,
    "overpower": 23.78,
    "is_valid": true,
    "timestamp": 0,
    "counters": [1,2,3],
    "total": 4
}

```

### Attributes ###

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`overpower`|     number     |       Value in Watts, on which an overpower condition is detected       |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|    Energy counter value for the last 3 round minutes in Watt-minute     |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

Shelly2: `/relay/{index}`
----------

```
GET /relay/0

{
    "ison": true,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "is_valid": false,
    "source": "http"
}

```

Shows current status of each output channel and accepts commands for controlling the channel. This is usable only when device mode is set to `relay` via [`/settings`](#shelly2-settings).

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                    Whether an overpower condition turned the channel OFF                     |
|   `is_valid`    | bool |                 Whether the associated power meter is functioning correctly                  |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly2: `/roller/{index}`
----------

```
GET /roller/0

{
    "state": "stop",
    "power": 0,
    "is_valid": false,
    "safety_switch": false,
    "overtemperature" false,
    "stop_reason": "normal",
    "last_direction": "stop",
    "current_pos": 90,
    "calibrating": false,
    "positioning": true
}

```

Controls the logical `roller` device and retrieves its current status. When `go=to_pos`, `roller_pos` must also be specified and valid.

### Attributes ###

|   Attribute    | Type |                                Description                                |
|----------------|------|---------------------------------------------------------------------------|
|    `state`     | bool |                      One of `stop`, `open`, `close`                       |
|    `power`     |number|                    Current power consumption in Watts                     |
|   `is_valid`   | bool |                   If the power meter functions properly                   |
|`safety_switch` | bool |              Whether the safety input is currently triggered              |
| `stop_reason`  | bool |Last cause for stopping: `normal`, `safety_switch`, `obstacle`, `overpower`|
|`last_direction`| bool |                Last direction of motion, `open` or `close`                |
| `current_pos`  |number|                        Current position in percent                        |
| `calibrating`  | bool |    Whether the device is currently performing a calibration procedure     |
| `positioning`  | bool |         Whether the device is calibrated for positioning control          |

### Parameters ###

| Parameter  | Type |                                                                                 Description                                                                                 |
|------------|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `go`    |string|                                                          Accepted values are `open`, `close`, `stop` and `to_pos`                                                           |
|`roller_pos`|number|                                                      Desired position in percent. Used in combination with `go=to_pos`                                                      |
| `duration` |number|If specified, the motor will move for this period in seconds. If missing, the value of `maxtime` in [`/settings/roller/{index}`](#shelly2-settings-roller-index) will be used|
|  `offset`  |number|                                                            Offset 0 - 100%. Use `offset` or `duration`, not both                                                            |

Shelly2: `/roller/{index}/calibrate`
----------

Since v1.4.0: Requesting this endpoint will trigger a calibration procedure to be performed. Shelly2 will measure the time it takes to open and close the mechanical device under control. Once this completes successfully, Shelly2 will be able to not only open and close, but target a specific position between the two.

Shelly2.5
==========

Shelly2.5: Overview
----------

Shelly2.5 is the improved successor to our popular Shelly2 model. The product page:

<https://shelly.cloud/products/shelly-25-smart-home-automation-relay/>

has all key features described, wiring diagram and User Manual.

Shelly2.5 can operate in two distinct device modes: **Relay** and**Roller Shutter**. Devices are initially programmed to work in **Relay** пode. The operating mode of Shelly2.5 can be set via the [`/settings`](#shelly2-5-settings) endpoint. Commands to perform actions can come from:

* A physical input switch (SW1/SW2)
* HTTP request, trough the local web interface
* A command sent via either Allterco's cloud service or MQTT messages
* A weekly-schedule event or a sunrise/sunset-generated event

Shelly2.5 supports up to 20 schedule rules.

### Factory Reset ###

To perform a factory reset on a Shelly2.5 device, do so by pressing the user button or relay input switches:

* hold the user button for 5 seconds to reset WiFi setup to AP mode
* hold the user button for 10 seconds to perform a complete factory reset
* flip an input switch quickly 5 times within the first minute after power on to perform a complete factory reset

Shelly2.5 in Relay Mode
----------

In **Relay** mode, each of the two channels is controlled individually and supports the **ON** and **OFF** commands.

Relay channels support `auto_on` and `auto_off` settings -- these are timers in seconds which will turn ON or OFF the channel when it has been turned OFF or ON respectively, from either a physical switch or network command. Thus, the user can set a limit for how long the channel can be **ON** or **OFF**.

Upon power-on, outputs are initialized using one of 4 available strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly, if the selected input type can provide this information

Physical input switches can be one of:

* a momentary, push-button switch
* a toggle switch with two stable states
* an "edge" switch. In this input mode, every switch state transition causes a toggle of the output state. This can be used with input from existing two-way switch installations
* detached, inputs do not control the relays
* activation switch -- each event turns the channel on and resets the auto-off timer

To control Shelly2.5 in **Relay** mode, use these resources:

* [`/settings/relay/{index}`](#shelly2-5-settings-relay-index) to configure the behavior of each channel
* [`/relay/{index}`](#shelly2-5-relay-index) to control and monitor the channel

Shelly2.5 in Roller Mode
----------

In **Roller** mode the device can be used to control a bi-directional motor, with optional obstacle detection and safety switch features. Commands are: **Open**, **Close**, **Stop** and **Set Position**.

Shelly2.5 has a single logical **Roller**, but we index the HTTP resources to allow for future devices with more output channels and **Roller**-s.

When Shelly2.5 is in **Roller** mode, use:

* [`/settings/roller/{index}`](#shelly2-5-settings-roller-index) to configure the behavior of this **Roller** controller, including the advanced features described below
* [`/roller/{index}`](#shelly2-5-roller-index) to query the state and send commands

### Obstacle detection ###

In **Roller** mode, the integrated power meter of Shelly2.5 can be used to detect motor overload which usually means something obstructing the movement of the door or roller shutter. A set of parameters define the behavior of Shelly2.5 when such event occurs. These are:

* the direction of motion for which obstacle detection is enabled
* the action to perform when the event occurs
* number of seconds to wait before triggering the condition -- motors draw big initial current which may be falsely interpreted as an obstacle

### Safety-switch input ###

While in **Roller** mode and when inputs are configured as `onebutton`, the second physical input can be used as a safety input -- it can be tied to an end-stop switch or user safety stop button. Its configuration parameters are:

* when to honor events on the safety input: during either direction or any direction of motion
* what to do when the switch is engaged:
  * stop the motion
  * pause the motion, so when the switch is disengaged it continues in the same direction

* which external commands are allowed while the safety inputs is engaged

### Position control ###

Shelly2.5 can be commanded to move the door (cover, sliding gate, etc.) to a relative position between fully open and completely closed. For this feature to work the device needs to perform a calibration procedure, measuring the time it takes for closing and opening. See [`/roller/{index}/calibrate`](#shelly2-5-roller-index-calibrate)

Shelly2.5: MQTT
----------

Shelly2.5 allows control and monitoring over MQTT for both relay and roller modes. Device mode, along with other parameters need to be configured using the mobile application or web interface. In either mode, Shelly2.5 reports:

* `shellies/shellyswitch25-<deviceid>/input/<i>` for each SW input `<i>`; reports the current state as `0` or `1`
* `shellies/shellyswitch25-<deviceid>/temperature` reports internal device temperature in °C
* `shellies/shellyswitch25-<deviceid>/overtemperature` reports `1` when device has overheated, normally `0`
* `shellies/shellyswitch25-<deviceid>/temperature_status` reports `Normal`, `High`, `Very High`
* `shellies/shellyswitch25-<deviceid>/voltage` reports the device voltage, in [V](ex.%20`230.00`)

### MQTT in Relay mode ###

Input events can be monitored on:

* `shellies/shellyswitch25-<deviceid>/longpush/<i>` for each SW input `<i>`; reports a value indicating longpush state as `0` (shortpush) or `1` (longpush)
* `shellies/shellyswitch25-<deviceid>/input_event/<i>` for each SW input `<i>`; reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly2-5-status) for details

In relay mode, the following topics can be used to read and set output channels `0` and `1`:

* `shellies/shellyswitch25-<deviceid>/relay/<i>` for each relay `<i>`; reports status: `on`, `off` or `overpower`
* `shellies/shellyswitch25-<deviceid>/relay/<i>/command` for each relay `<i>`; accepts `on`, `off` or `toggle`

The device measures energy flow for each channel and reports these values on:

* `shellies/shellyswitch25-<deviceid>/relay/<i>/power` for each relay `<i>`; reports instantaneous power consumption rate in Watts
* `shellies/shellyswitch25-<deviceid>/relay/<i>/energy` for each relay `<i>`; reports amount of energy consumed in Watt-minute
* `shellies/shellyswitch25-<deviceid>/relay/<i>/overpower_value` for each relay `<i>` reports the value in Watts, on which an overpower condition is detected

### MQTT in Roller mode ###

When configured to operate in roller mode, MQTT topics used by Shelly2.5 are:

* `shellies/shellyswitch25-<deviceid>/roller/0` reports the current state: `open` or `close` while in motion, `stop` when not moving
* `shellies/shellyswitch25-<deviceid>/roller/0/command` accepts `rc` (performs roller calibration), `open`, `close` and `stop`

* `shellies/shellyswitch25-<deviceid>/roller/0/power` reports instantaneous power consumption rate in Watts

* `shellies/shellyswitch25-<deviceid>/roller/0/energy` reports amount of energy consumed in Watt-minute

For position control to work the device must be successfully calibrated, so that the time it takes for closing and opening are known.

* `shellies/shellyswitch25-<deviceid>/roller/0/pos` reports the current position in percent, `-1` if invalid
* `shellies/shellyswitch25-<deviceid>/roller/0/command/pos` accepts a number between 0 and 100, which is the target position in percent

Shelly2.5: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly 2.5 SHSW-25 relay-mode](docs/coiot/v2/examples/Shelly%202.5%20SHSW-25%20relay-mode)
* [Shelly 2.5 SHSW-25 roller-mode](docs/coiot/v2/examples/Shelly%202.5%20SHSW-25%20roller-mode)

Shelly2.5: `/settings`
----------

```
GET /settings

{
    "factory_reset_from_switch": true,
    "mode": "relay",
    "max_power": 1840,
    "longpush_time": 1000,
    "led_status_disable": false,
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "btn_off_url",
            "out_on_url",
            "out_off_url",
            "longpush_url",
            "shortpush_url",
            "roller_open_url",
            "roller_close_url",
            "roller_stop_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "switch",
            "btn_type": "toggle",
            "btn_reverse": 0,
            "auto_on": 0,
            "auto_off": 0,
            "max_power": 0,
            "schedule": false,
            "schedule_rules": []
        },
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "switch",
            "btn_type": "toggle",
            "btn_reverse": 0,
            "auto_on": 0,
            "auto_off": 0,
            "max_power": 0,
            "schedule": false,
            "schedule_rules": []
        }
    ],
    "rollers": [
        {
            "maxtime": 20,
            "maxtime_open": 20,
            "maxtime_close": 20,
            "default_state": "stop",
            "swap": false,
            "swap_inputs": false,
            "input_mode": "openclose",
            "button_type": "toggle",
            "btn_reverse": 0,
            "state": "stop",
            "power": 0,
            "is_valid": false,
            "safety_switch": false,
            "schedule": false,
            "schedule_rules": [],
            "obstacle_mode": "disabled",
            "obstacle_action": "stop",
            "obstacle_power": 200,
            "obstacle_delay": 1,
            "ends_delay": 2000,
            "safety_mode": "while_opening",
            "safety_action": "stop",
            "safety_allowed_on_trigger": "none",
            "off_power": 2,
            "positioning": true
        }
    ],
    "favorites_enabled": true,
    "favorites": [
      {
        "name": "Fav1",
        "pos": 55
      },
      {
        "name": "Fav2",
        "pos": 100
      },
      {
        "name": "Fav3",
        "pos": 20
      },
      {
        "name": "Fav4",
        "pos": 40
      }
    ]
}

```

Shelly2.5 extends the common `/settings` endpoint with relay and roller-mode specific data, power consumption status and contains the settings for this device's **Relays** and **Rollers** and adds [`/settings/relay/{index}`](#shelly2-5-settings-relay-index) and [`/settings/roller/{index}`](#shelly2-5-settings-roller-index) for setting the parameters.

### Attributes ###

|         Attribute         |     Type      |                                                                                         Description                                                                                         |
|---------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|     bool      |                                                             Whether factory reset via 5-time flip of an input switch is enabled                                                             |
|          `mode`           |    string     |                                                                                     `relay` or `roller`                                                                                     |
|   `led_status_disable`    |     bool      |                                                                          Whether LED status indication is enabled                                                                           |
|        `max_power`        |    number     |Overpower threshold in Watts for `roller` mode only. For `relay` mode the device keeps separate, per-channel configurations, see [`/settings/relay/{index}`](#shelly2-5-settings-relay-index)|
|      `longpush_time`      |    number     |                                                                             Duration to detect long push, `ms`                                                                              |
|         `actions`         |     hash      |                               List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly2-5-settings-actions)                                |
|         `relays`          |array of hashes|                                                 See [`/settings/relay/{index}`](#shelly2-5-settings-relay-index) for explanation of values                                                  |
|         `rollers`         |array of hashes|                                                See [`/settings/roller/{index}`](#shelly2-5-settings-roller-index) for explanation of values                                                 |
|        `favorites`        |array of hashes|                                             See [`/settings/favorites/{index}`](#shelly2-5-settings-favorites-index) for explanation of values                                              |

### Parameters ###

|         Parameter         | Type |                                                                                           Description                                                                                           |
|---------------------------|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |                                                                 Enable/disable factory reset via 5-time flip of an input switch                                                                 |
|          `mode`           |string|                                                                    Set device mode. Accepted values are `relay` and `roller`                                                                    |
|   `led_status_disable`    | bool |                                                                                  Disable LED status indication                                                                                  |
|        `max_power`        |number|Set overpower threshold in Watts for `roller` mode only. For `relay` mode the device keeps separate, per-channel configurations, see [`/settings/relay/{index}`](#shelly2-5-settings-relay-index)|
|         `actions`         | hash |                                                           For setting actions, see [`/settings/actions`](#shelly2-5-settings-actions)                                                           |
|      `longpush_time`      |number|                                                                          Set duration to detect long push, `1..5000ms`                                                                          |
|    `favorites_enabled`    | bool |                                                                         **roller mode only** Enable favourite positions                                                                         |

Shelly2.5: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "roller_open_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "roller_close_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "roller_stop_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly2.5 supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action      |Index|                                                     Description                                                      |
|------------------|-----|----------------------------------------------------------------------------------------------------------------------|
|   `btn_on_url`   | 0-1 |                                       URL to access when SW input is activated                                       |
|  `btn_off_url`   | 0-1 |                                      URL to access when SW input is deactivated                                      |
|   `out_on_url`   | 0-1 |                                        URL to access when output is activated                                        |
|  `out_off_url`   | 0-1 |                                       URL to access when output is deactivated                                       |
|  `longpush_url`  | 0-1 |URL to access on longpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`. |
| `shortpush_url`  | 0-1 |URL to access on shortpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`.|
|`roller_open_url` |  0  |                                          URL to access when roller is open                                           |
|`roller_close_url`|  0  |                                         URL to access when roller is closed                                          |
|`roller_stop_url` |  0  |                                         URL to access when roller is stopped                                         |

Shelly2.5: `/settings/relay/{index}`
----------

```
GET /settings/relay/0

{
    "name": null,
    "appliance_type": "General",
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "btn_type": "toggle",
    "btn_reverse": 0,
    "auto_on": 0,
    "auto_off": 0,
    "max_power": 2300,
    "schedule": false,
    "schedule_rules": []
}

```

The returned document here is identical to the data returned in `/settings` for the particular output channel in the `relays` array. The attributes match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                                              Description                                               |
|----------------|----------------|--------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                               Relay name                                               |
|`appliance_type`|     string     |                                   Custom configurable appliance type                                   |
|     `ison`     |      bool      |                                             Channel state                                              |
|  `has_timer`   |      bool      |                            Whether there is an active timer on the channel                             |
|  `overpower`   |      bool      |                              Whether an overpower condition has occurred                               |
|`default_state` |     string     |                      Default power-on state, one of `off`, `on`, `last`, `switch`                      |
|   `btn_type`   |     string     |Button type, one of `momentary`, `toggle`, `edge`, `detached`, `action`, `cycle`, `momentary_on_release`|
| `btn_reverse`  |     number     |                                 Whether input switch state is inverted                                 |
|   `auto_on`    |     number     |             Automatic flip back timer, seconds. Will engage after turning the channel OFF              |
|   `auto_off`   |     number     |              Automatic flip back timer, seconds. Will engage after turning the channel ON              |
|  `max_power`   |     number     |                         Per-channel overpower threshold (used in `relay` mode)                         |
|   `schedule`   |      bool      |                                     Whether scheduling is enabled                                      |
|`schedule_rules`|array of strings|                                     Rules for schedule activation                                      |

### Parameters ###

|   Parameter    |      Type      |                                             Description                                             |
|----------------|----------------|-----------------------------------------------------------------------------------------------------|
|    `reset`     |      any       | Submitting a non-empty value will reset settings for this relay output channel to factory defaults  |
|     `name`     |     string     |                                             Relay name                                              |
|`appliance_type`|     string     |                               Set custom configurable appliance type                                |
|`default_state` |     string     |                           Accepted values: `off`, `on`, `last`, `switch`                            |
|   `btn_type`   |     string     |Accepted values: `momentary`, `toggle`, `edge`, `detached`, `action`, `cycle`, `momentary_on_release`|
| `btn_reverse`  |      bool      |                                    Invert the input switch state                                    |
|   `auto_on`    |     number     |            Automatic flip back timer, seconds. Will engage after turning the channel OFF            |
|   `auto_off`   |     number     |            Automatic flip back timer, seconds. Will engage after turning the channel ON             |
|  `max_power`   |     number     |                     Set per-channel overpower threshold (used in `relay` mode)                      |
|   `schedule`   |      bool      |              Enable or disable schedules and sunrise/sunset commands for this channel               |
|`schedule_rules`|array of strings|                        Rules for schedule activation, e.g. `0000-0123456-on`                        |

Shelly2.5: `/settings/roller/{index}`
----------

```
GET /settings/roller/0

{
    "maxtime": 20,
    "maxtime_open": 0,
    "maxtime_close": 0,
    "default_state": "stop",
    "swap": false,
    "swap_inputs": false,
    "input_mode": "openclose",
    "button_type": "toggle",
    "btn_reverse": 0,
    "state": "stop",
    "power": 0,
    "is_valid": true,
    "safety_switch": false,
    "schedule": false,
    "schedule_rules": [],
    "obstacle_mode": "disabled",
    "obstacle_action": "stop",
    "obstacle_power": 200,
    "obstacle_delay": 1,
    "ends_delay": 2000,
    "safety_mode": "while_opening",
    "safety_action": "stop",
    "safety_allowed_on_trigger": "none",
    "off_power": 2,
    "positioning": true
}

```

The returned document here is identical to the data returned in `/settings` as a hash in the `rollers`. The attributes match the set of accepted parameters.

### Attributes ###

|         Attribute         |      Type      |                                                                       Description                                                                        |
|---------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|         `maxtime`         |     number     |                                      The maximum time needed for the mechanism to completely open or close, seconds                                      |
|      `maxtime_open`       |     number     |                                          The maximum time needed for the mechanism to completely open, seconds                                           |
|      `maxtime_close`      |     number     |                                          The maximum time needed for the mechanism to completely close, seconds                                          |
|      `default_state`      |     string     |                                   One of `stop`, `open`, `close`. This parameters determines the behavior on power-on                                    |
|          `swap`           |      bool      |                                                        Whether to swap OPEN and CLOSE directions                                                         |
|       `swap_inputs`       |      bool      |                                                                Whether inputs are swapped                                                                |
|       `input_mode`        |     string     |One of `openclose` -- each input controls one direction of motion, `onebutton` -- a single button press cycles through states: open, stop, close, stop ...|
|       `button_type`       |     string     |                                                   One of `momentary`, `toggle`, `detached` or `action`                                                   |
|       `btn_reverse`       |     number     |                                            Whether to invert the state of input switch before interpreting it                                            |
|          `state`          |      bool      |                                                              One of `stop`, `open`, `close`                                                              |
|          `power`          |     number     |                                                            Current power consumption in Watts                                                            |
|        `is_valid`         |      bool      |                                                          If the power meter functions properly                                                           |
|      `safety_switch`      |      bool      |                                                     Whether the safety input is currently triggered                                                      |
|        `schedule`         |      bool      |                                                              Whether scheduling is enabled                                                               |
|     `schedule_rules`      |array of strings|                                                              Rules for schedule activation                                                               |
|      `obstacle_mode`      |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|     `obstacle_action`     |     string     |                                                                 One of `stop`, `reverse`                                                                 |
|     `obstacle_power`      |     number     |                                               Power threshold for triggering `"obstacle"` condition, Watts                                               |
|     `obstacle_delay`      |     number     |                               Number of seconds to wait after powering on the motor before obstacle detection is activated                               |
|       `ends_delay`        |     number     |                            Period in ms after which the roller decides that it can't move anymore, 0-10000, with step of 100                             |
|       `safety_mode`       |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|      `safety_action`      |     string     |                                                            One of `stop`, `pause`, `reverse`                                                             |
|`safety_allowed_on_trigger`|     string     |                             Which commands are allowed while the safety switch is triggered: `none`, `open`, `close`, `all`                              |
|        `off_power`        |     number     |                      Power value below which the roller is considered "stopped", i.e. the actuator is stopped by an end-stop switch                      |
|       `positioning`       |      bool      |                                                 Whether the device is calibrated for positioning control                                                 |

### Parameters ###

|         Parameter         |      Type      |                                                                       Description                                                                        |
|---------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|          `reset`          |      any       |                                     Submitting a non-empty value will reset **Roller** settings to factory defaults                                      |
|         `maxtime`         |     number     |                                      The maximum time needed for the mechanism to completely open or close, seconds                                      |
|      `maxtime_open`       |     number     |                                          The maximum time needed for the mechanism to completely open, seconds                                           |
|      `maxtime_close`      |     number     |                                          The maximum time needed for the mechanism to completely close, seconds                                          |
|      `default_state`      |     string     |                                   One of `stop`, `open`, `close`. This parameters determines the behavior on power-on                                    |
|          `swap`           |      bool      |                                                        Whether to swap OPEN and CLOSE directions                                                         |
|       `swap_inputs`       |      bool      |                                                                       Swap inputs                                                                        |
|       `input_mode`        |     string     |One of `openclose` -- each input controls one direction of motion, `onebutton` -- a single button press cycles through states: open, stop, close, stop ...|
|        `btn_type`         |     string     |                                                   One of `momentary`, `toggle`, `detached` or `action`                                                   |
|       `btn_reverse`       |      bool      |                                            Whether to invert the state of input switch before interpreting it                                            |
|        `schedule`         |      bool      |                                         Enable or disable schedules and sunrise/sunset commands for this channel                                         |
|     `schedule_rules`      |array of strings|                                                  Rules for schedule activation, e.g. `0000-0123456-on`                                                   |
|      `obstacle_mode`      |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|     `obstacle_action`     |     string     |                                                                 One of `stop`, `reverse`                                                                 |
|     `obstacle_power`      |     number     |                                                Power threshold for triggering "obstacle" condition, Watts                                                |
|     `obstacle_delay`      |     number     |                               Number of seconds to wait after powering on the motor before obstacle detection is activated                               |
|       `ends_delay`        |     number     |                            Period in ms after which the roller decides that it can't move anymore, 0-10000, with step of 100                             |
|        `off_power`        |     number     |                      Power value below which the roller is considered "stopped", i.e. the actuator is stopped by an end-stop switch                      |
|       `positioning`       |     number     |                                     Whether position control is possible (calibration was performed and successful)                                      |
|       `safety_mode`       |     string     |                                           One of `disabled`, `while_opening`, `while_closing`, `while_moving`                                            |
|      `safety_action`      |     string     |                                                            One of `stop`, `pause`, `reverse`                                                             |
|`safety_allowed_on_trigger`|     string     |                             Which commands are allowed while the safety switch is triggered: `none`, `open`, `close`, `all`                              |

Shelly2.5: `/settings/favorites/{index}`
----------

```
GET /settings/favorites/0

{
    "name": "Fav3",
    "pos": 20
}

```

### Attributes ###

|Attribute| Type |         Description         |
|---------|------|-----------------------------|
| `name`  |string|Name of the favorite position|
|  `pos`  | num  |Position in %, from 0 to 100 |

### Parameters ###

|Parameter| Type |           Description           |
|---------|------|---------------------------------|
| `name`  |string|Set name of the favorite position|
|  `pos`  | num  |Set position in %, from 0 to 100 |

Shelly2.5: `/status`
----------

```
GET /status (in relay mode)

{
    "relays": [
        {
            "ison": false,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "overtemperature": false,
            "is_valid": true,
            "source": "http"
        },
        {
            "ison": false,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "overtemperature": false,
            "is_valid": true,
            "source": "cloud"
        }
    ],
    "meters": [
        {
            "power": 0,
            "overpower": 23.78,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        },
        {
            "power": 0,
            "overpower": 23.78,
            "is_valid": true,
            "timestamp": 0,
            "counters": [5,6,7],
            "total": 8
        }
    ],
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        },
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        }
    ],
    "temperature": 37.04,
    "overtemperature": false,
    "tmp": {
        "tC": 37.04,
        "tF": 98.67,
        "is_valid": true
    },
    "temperature_status": "Normal"
}

```

Shelly2.5 adds information about the current state of the output channels, the logical "roller" device and power metering.

### Attributes ###

|     Attribute      |     Type      |                                                                              Description                                                                              |
|--------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      `relays`      |array of hashes|  Displayed in **Relay** mode: Contains the current state of the relay output channels. See [`/relay/{index}`](#shelly2-5-relay-index) for description of attributes   |
|     `rollers`      |array of hashes|Displayed in **Roller** mode: Contains the current state of the logical "roller" device. See [`/roller/{index}`](#shelly2-5-roller-index) for description of attributes|
|      `meters`      |array of hashes|                                                       Current status of the power meters, see description below                                                       |
|      `inputs`      |array of hashes|                                                          Current state of the inputs, see description below                                                           |
|   `temperature`    |    number     |                                                                       Device temperature in °C                                                                        |
| `overtemperature`  |     bool      |                                                           Whether an overtemperature condition has occurred                                                           |
|      `tmp.tC`      |    number     |                                                                       Device temperature in °C                                                                        |
|      `tmp.tF`      |    number     |                                                                       Device temperature in °F                                                                        |
|   `tmp.is_valid`   |     bool      |                                                                  Whether device temperature is valid                                                                  |
|`temperature_status`|    string     |                                                   Temperature status of the device, "Normal", "High" or "Very High"                                                   |

### `inputs.{index}` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Input events are only detected in `relay` mode and only when `btn_type` is configured as `momentary`, `momentary_on_release` or `detached`.

Shelly2.5: `/meter/{index}`
----------

```
GET /meter/0

{
    "power": 0,
    "overpower": 23.78,
    "is_valid": true,
    "timestamp": 0,
    "counters": [1,2,3],
    "total": 4
}

```

### Attributes ###

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`overpower`|     number     |       Value in Watts, on which an overpower condition is detected       |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|    Energy counter value for the last 3 round minutes in Watt-minute     |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

Shelly2.5: `/relay/{index}`
----------

```
GET /relay/0

{
    "ison": true,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "overtemperature": false,
    "is_valid": false,
    "source": "http"
}

```

Shows current status of each output channel and accepts commands for controlling the channel. This is usable only when device mode is set to `relay` via [`/settings`](#shelly2-5-settings).

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                    Whether an overpower condition turned the channel OFF                     |
|`overtemperature`| bool |                        Whether an overtemperature condition occurred                         |
|   `is_valid`    | bool |                 Whether the associated power meter is functioning correctly                  |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly2.5: `/roller/{index}`
----------

```
GET /roller/0

{
    "state": "stop",
    "power": 0,
    "is_valid": false,
    "safety_switch": false,
    "overtemperature": false,
    "stop_reason": "normal",
    "last_direction": "stop",
    "current_pos": 90,
    "calibrating": false,
    "positioning": true
}

```

Controls the logical "roller" device and retrieves its current status. When `go=to_pos`, `roller_pos` must also be specified and valid.

### Attributes ###

|    Attribute    | Type |                                Description                                |
|-----------------|------|---------------------------------------------------------------------------|
|     `state`     |string|                      One of `stop`, `open`, `close`                       |
|     `power`     |number|                    Current power consumption in Watts                     |
|   `is_valid`    | bool |                   If the power meter functions properly                   |
| `safety_switch` | bool |              Whether the safety input is currently triggered              |
|`overtemperature`| bool |               Whether an overtemperature condition occurred               |
|  `stop_reason`  | bool |Last cause for stopping: `normal`, `safety_switch`, `obstacle`, `overpower`|
|`last_direction` | bool |                Last direction of motion, `open` or `close`                |
|  `current_pos`  |number|                        Current position in percent                        |
|  `calibrating`  | bool |    Whether the device is currently performing a calibration procedure     |
|  `positioning`  | bool |         Whether the device is calibrated for positioning control          |

### Parameters ###

| Parameter  | Type |                                                                                  Description                                                                                  |
|------------|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `go`    |string|                                                           Accepted values are `open`, `close`, `stop` and `to_pos`                                                            |
|`roller_pos`|number|                                                       Desired position in percent. Used in combination with `go=to_pos`                                                       |
| `duration` |number|If specified, the motor will move for this period in seconds. If missing, the value of `maxtime` in [`/settings/roller/{index}`](#shelly2-5-settings-roller-index) will be used|
|  `offset`  |number|                                                             Offset 0 - 100%. Use `offset` or `duration`, not both                                                             |

Shelly2.5: `/roller/{index}/calibrate`
----------

Requesting this endpoint will trigger a calibration procedure to be performed. Shelly2.5 will measure the time it takes to open and close the mechanical device under control. Once this completes successfully, Shelly2.5 will be able to not only open and close, but target a specific position between the two. The procedure will open and close the actuated cover (door, roller shutter, etc.) detecting when an end position is reached. The average times for opening and closing will be stored by the device and used when a `go=to_pos` command is issued.

Shelly Motion
==========

Shelly Motion: Overview
----------

Shelly Motion is a WiFi Smart motion sensor with long battery life and constant connection to WiFi:

<https://shelly.cloud/shelly-motion-smart-home-automation-sensor/>

Shelly Motion is always WiFi connected.

The device comes from the factory in off state. When the user button is pressed, the device switches on a "setup" mode -- it will remain turned on for 3 minutes, allowing configuration over the web interface. Once configured to connect to a WiFi network, it remains in active mode always connected to the WiFi.

### Actions ###

Shelly Motion supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action      |                               Description                                |
|------------------|--------------------------------------------------------------------------|
|   `motion_on`    |                    URL(s) to invoke on motion events                     |
|  `motion_dark`   |        URL(s) to invoke when motion is detected in dark condition        |
|`motion_twilight` |      URL(s) to invoke when motion is detected in twilight condition      |
| `motion_bright`  |       URL(s) to invoke when motion is detected in bright condition       |
|   `motion_off`   |URL(s) to invoke when no motion is detected and the blind time has elapsed|
|`tamper_alarm_on` |               URL(s) to invoke when vibration is detected                |
|`tamper_alarm_off`|               URL(s) to invoke when vibration has finished               |

### Factory Reset ###

To restore Shelly Motion to its factory settings, turn the device on if needed, then press and hold the user button for \> 10 seconds. The device will reboot with the factory defaults into AP mode.

Shelly Motion: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly Motion sends values from its internal sensors on the following topics:

* `shellies/shellymotionsensor-<deviceid>/info`: publishes a JSON payload with the content of HTTP `/status` endpoint

Shelly Motion: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Motion SHMOS-01](docs/coiot/v2/examples/Shelly%20Motion%20SHMOS-01)

Shelly Motion: `/settings`
----------

```
GET /settings

{
    "schedule": false,
    "schedule_rules": [],
    "mode":"sensor",
    "motion": {
        "sensitivity": 100,
        "blind_time_minutes": 1,
        "pulse_count": 2,
        "operating_mode": 0,
        "enabled": true
    },
    "sleep_time": 0,
    "tamper_sensitivity": 2,
    "led_status_disable": false,
    "dark_threshold": 100,
    "twilight_threshold": 500,
    "sleep_mode":{
      "period":60,
      "unit":"m"
    }
}

```

### Attributes ###

|         Attribute         |      Type      |                                                  Description                                                  |
|---------------------------|----------------|---------------------------------------------------------------------------------------------------------------|
|       `sleep_time`        |     number     |                       If set, the device stays in inactive state for the remaining time                       |
|   `motion.sensitivity`    |     number     |                  Motion detection threshold. Lower value means higher sensitivity. `1..256`                   |
|`motion.blind_time_minutes`|     number     |            Time in minutes after the last motion to enable reporting a new motion event. `1..1440`            |
|   `motion.pulse count`    |     number     |                Number of consecutive motions in a short period to report motion event. `1..4`                 |
|  `motion.operating mode`  |     number     |Sets the operating mode for the sensor depending on light conditions. One of (Any/Dark/Twilight/Bright). `0..3`|
|     `motion.enabled`      |      bool      |                                Motion detection is enabled. `true` or `false`.                                |
|   `tamper_sensitivity`    |     number     |  Tamper (vibration) detection threshold. Lower value sets higher sensitivity. `1..127`, `0` - for disabled.   |
|   `led_status_disable`    |      bool      |                               Disable LEDs on device if set. `true` or `false`.                               |
|     `dark_threshold`      |     number     |                               Illumination level threshold for dark condition.                                |
|   `twilight_threshold`    |     number     |                             Illumination level threshold for twilight condition.                              |
|        `schedule`         |      bool      |                                         Whether scheduling is enabled                                         |
|     `schedule_rules`      |array of strings|                                         Rules for schedule activation                                         |

### Parameters ###

|         Parameter         |      Type      |                                                 Description                                                 |
|---------------------------|----------------|-------------------------------------------------------------------------------------------------------------|
|       `sleep_time`        |     number     |                         Set how long the device stays in inactive state, in seconds                         |
|   `motion_sensitivity`    |     number     |                                      Set motion sensitivity, `1..256`                                       |
|`motion_blind_time_minutes`|     number     |                                          Set blind time, `1..1440`                                          |
|   `motion_pulse_count`    |     number     |                                           Set pulse count, `1..4`                                           |
|  `motion_operating_mode`  |     number     |                        Set operating mode, one of (Any/Dark/Twilight/Bright) `0..3`                         |
|      `motion_enable`      |      bool      |                                       Enable/disable motion detection                                       |
|     `dark_threshold`      |     number     |                             Set illumination level threshold for dark condition                             |
|   `twilight_threshold`    |     number     |                           Set illumination level threshold for twilight condition                           |
|   `tamper_sensitivity`    |     number     |Set tamper (vibration) detection threshold. Lower value sets higher sensitivity. `1..127`, `0` - for disabled|
|   `led_status_disable`    |      bool      |                              Disable LEDs on device if set. `true` or `false`.                              |
|        `schedule`         |      bool      |                  Enable or disable schedules and sunrise/sunset commands for this channel                   |
|     `schedule_rules`      |array of strings|                            Rules for schedule activation, e.g. `0000-0123456-on`                            |

Shelly Motion: `/status`
----------

```
GET /status

{
    "lux": {
        "value": 1334,
        "illumination": "dark",
        "is_valid": true
    },
    "sensor": {
        "motion": false,
        "vibration": false,
        "timestamp": 317419479,
        "active": true,
        "is_valid": true
    },
    "bat": {
        "value": 21,
        "voltage": 3.096,
    },
    "charger": false,
    "timestamp": 317419479
}

```

Sensor values are reported on the `/status` endpoint.

### Attributes ###

|    Parameter     | Type |                              Description                              |
|------------------|------|-----------------------------------------------------------------------|
|   `lux.value`    |number|              Illumination measure by the sensor in lux.               |
|`lux.illumination`|string|                  One of `dark`, `twilight`, `bright`                  |
| `sensor.motion`  | bool |  Motion has been detected and the sensor blind time has not elapsed   |
|`sensor.vibration`| bool |Tamper (vibration) has been detected. Cleared after vibration has gone.|
| `sensor.active`  | bool |                  Whether motion detection is active                   |
|  `bat.voltage`   |number|                       Measured battery voltage                        |
|   `bat.value`    |number|                       battery charge in percent                       |
|    `charger`     | bool |                      Whether a charger connected                      |
|  `*.timestamp`   |number|                       Current device unix time                        |
|   `*.is_valid`   | bool |                 Whether motion sensor self-checks OK                  |

Shelly Motion: `/poweroff`
----------

Requesting this endpoint will power off the device. It can be turned back on by pressing the user button.

Shelly Motion 2
==========

Shelly Motion 2: Overview
----------

Shelly Motion 2 is a WiFi smart motion and temperature sensor with long battery life:

Shelly Motion 2 is always WiFi connected.

The device comes from the factory in off state. When the user button is pressed, the device switches on a "setup" mode -- it will remain turned on for 3 minutes, allowing configuration over the web interface. Once configured to connect to a WiFi network, it remains in active mode always connected to the WiFi.

### Actions ###

Shelly Motion 2 supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action      |                                      Description                                      |
|------------------|---------------------------------------------------------------------------------------|
|   `motion_on`    |                           URL(s) to invoke on motion events                           |
|  `motion_dark`   |              URL(s) to invoke when motion is detected in dark condition               |
|`motion_twilight` |            URL(s) to invoke when motion is detected in twilight condition             |
| `motion_bright`  |             URL(s) to invoke when motion is detected in bright condition              |
|   `motion_off`   |      URL(s) to invoke when no motion is detected and the blind time has elapsed       |
|`tamper_alarm_on` |                      URL(s) to invoke when vibration is detected                      |
|`tamper_alarm_off`|                     URL(s) to invoke when vibration has finished                      |
| `temp_over_url`  |                URL(s) to invoke when temperature \> `temp_over_value`                 |
| `temp_under_url` |                URL(s) to invoke when temperature \< `temp_under_value`                |
|   `report_url`   |URL(s) to report sensor events on `(/?hum=60&temp=25.00&id=shellymotionsensor2-xxxxxx)`|

### Factory Reset ###

To restore Shelly Motion 2 to its factory settings, turn the device on if needed, then press and hold the user button for \> 10 seconds. The device will reboot with the factory defaults into AP mode.

Shelly Motion 2: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly Motion 2 sends values from its internal sensors on the following topics:

* `shellies/shellymotion2-<deviceid>/info`: publishes a JSON payload with the content of HTTP `/status` endpoint

Shelly Motion 2: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Motion 2 SHMOS-02](docs/coiot/v2/examples/Shelly%20Motion%202%20SHMOS-02)

Shelly Motion 2: `/settings`
----------

```
GET /settings

{
    "device": {
        "type": "SHMOS-02",
        "mac": "84FD276ED988",
        "hostname": "shellymotion2-84FD276ED988",
        "num_outputs": 0
    },
    "wifi_ap": {
        "enabled": false,
        "ssid": "shellymotion2-84FD276ED988"
    },
    "wifi_sta": {
        "enabled": true,
        "ssid": "topcho",
        "ipv4_method": "dhcp",
        "ip": null,
        "gw": null,
        "mask": null,
        "dns": null
    },
    "mqtt": {
        "enable": false,
        "server": "192.168.33.2:1883",
        "user": null,
        "id": "shellymotion2-84FD276ED988",
        "clean_session": true,
        "max_qos": 0,
        "retain": false,
        "update_period": 60
    },
    "sntp": {
        "server": "time.google.com",
        "enabled": true
    },
    "login": {
        "enabled": false,
        "unprotected": false,
        "username": "admin",
        "default_username": "admin"
    },
    "pin_code": "",
    "name": null,
    "fw": "20220324-131952/master@383eea08+",
    "discoverable": true,
    "build_info": {
        "build_id": "20220324-131952/master@383eea08+",
        "build_timestamp": "2022-03-24T13:19:52Z",
        "build_version": "2022032413"
    },
    "cloud": {
        "enabled": false
    },
    "coiot": {
        "enabled": false,
        "update_period": 3600,
        "peer": ""
    },
    "timezone": "Europe/Sofia",
    "lat": 42.660530,
    "lng": 23.382280,
    "tzautodetect": false,
    "tz_utc_offset": 7200,
    "tz_dst": false,
    "tz_dst_auto": true,
    "time": "12:46",
    "sleep_time": 0,
    "motion": {
        "sensitivity": 189,
        "blind_time_minutes": 5,
        "pulse_count": 1,
        "operating_mode": 0,
        "enabled": true
    },
    "led_status_disable": false,
    "tamper_sensitivity": 2,
    "dark_threshold": 100,
    "twilight_threshold": 500,
    "schedule": false,
    "schedule_rules": [],
    "hwinfo": {
        "hw_revision": "dev-prototype",
        "batch_id": 0
    },
    "sleep_mode": {
        "period": 60,
        "unit": "m"
    },
    "sensors": {
        "temperature_unit": "C",
        "temperature_threshold": 0.0
    },
    "temperature_offset": 0.0
}

```

### Attributes ###

|           Attribute            |      Type      |                                                  Description                                                  |
|--------------------------------|----------------|---------------------------------------------------------------------------------------------------------------|
|          `sleep_time`          |     number     |                      If set, the device stays in inactive state for the remaining time.                       |
|      `motion.sensitivity`      |     number     |                  Motion detection threshold. Lower value means higher sensitivity. `1..256`                   |
|  `motion.blind_time_minutes`   |     number     |            Time in minutes after the last motion to enable reporting a new motion event. `1..1440`            |
|      `motion.pulse count`      |     number     |                Number of consecutive motions in a short period to report motion event. `1..4`                 |
|    `motion.operating mode`     |     number     |Sets the operating mode for the sensor depending on light conditions. One of (Any/Dark/Twilight/Bright). `0..3`|
|        `motion.enabled`        |      bool      |                                Motion detection is enabled. `true` or `false`.                                |
|      `tamper_sensitivity`      |     number     |  Tamper (vibration) detection threshold. Lower value sets higher sensitivity. `1..127`, `0` - for disabled.   |
|      `led_status_disable`      |      bool      |                               Disable LEDs on device if set. `true` or `false`.                               |
|        `dark_threshold`        |     number     |                               Illumination level threshold for dark condition.                                |
|      `twilight_threshold`      |     number     |                             Illumination level threshold for twilight condition.                              |
|           `schedule`           |      bool      |                                        Whether scheduling is enabled.                                         |
|        `schedule_rules`        |array of strings|                                        Rules for schedule activation.                                         |
|       `wifi_ap.enabled`        |      bool      |                                      Whether the device's AP is enabled.                                      |
|       `wifi_sta.enabled`       |      bool      |                                           Whether Wi-Fi is enabled.                                           |
|         `mqtt.enable`          |      bool      |                                           Whether MQTT is enabled.                                            |
|         `sntp.server`          |     string     |                                             Sets the SNTP server.                                             |
|         `sntp.enabled`         |      bool      |                                           Whether SNTP is enabled.                                            |
|        `login.enabled`         |      bool      |                           Whether the requirement for login credentials is enabled.                           |
|      `login.unprotected`       |      bool      |                                     Whether unprotected login is enabled.                                     |
|        `login.username`        |     string     |                                              Sets the username.                                               |
|    `login.default_username`    |     string     |                                          Sets the default username.                                           |
|         `discoverable`         |      bool      |                                      Whether the device is discoverable.                                      |
|        `cloud.enabled`         |      bool      |                                         Whether the cloud is enabled.                                         |
|        `coiot.enabled`         |      bool      |                                           Whether CoIoT is enabled.                                           |
|     `coiot.update_period`      |     number     |                         The period of time in milliseconds before each CoIoT update.                          |
|           `timezone`           |     string     |                                          Sets the device's timezone.                                          |
|             `time`             |     string     |                                               The current time.                                               |
|        `tz_auto_detect`        |      bool      |                                Whether autodetecting the timezone is enabled.                                 |
|        `tz_utc_offset`         |     number     |                               The offset from the UTC timezone in milliseconds.                               |
|      `sleep_mode.period`       |     number     |                     Periodic update period in `sleep_mode.unit`. Value cannot be changed.                     |
|       `sleep_mode.unit`        |     string     |                                     `m` or `h`. Value cannot be changed.                                      |
|   `sensors.temperature_unit`   |     string     |                                    `C` for Celsius or `F` for Fahrenheit.                                     |
|`sensors.temperature_threshohld`|     number     |                             Temperature delta (in °C), which triggers an update.                              |
|      `temperature_offset`      |     number     |                                          Temperature offset (in °C).                                          |

### Parameters ###

|           Parameter            |      Type      |                                                 Description                                                  |
|--------------------------------|----------------|--------------------------------------------------------------------------------------------------------------|
|          `sleep_time`          |     number     |                         Set how long the device stays in inactive state, in seconds.                         |
|      `motion_sensitivity`      |     number     |                                      Set motion sensitivity, `1..256`.                                       |
|  `motion_blind_time_minutes`   |     number     |                                          Set blind time, `1..1440`.                                          |
|      `motion_pulse_count`      |     number     |                                           Set pulse count, `1..4`.                                           |
|    `motion_operating_mode`     |     number     |                        Set operating mode, one of (Any/Dark/Twilight/Bright) `0..3`.                         |
|        `motion_enable`         |      bool      |                                       Enable/disable motion detection.                                       |
|        `dark_threshold`        |     number     |                             Set illumination level threshold for dark condition.                             |
|      `twilight_threshold`      |     number     |                           Set illumination level threshold for twilight condition.                           |
|      `tamper_sensitivity`      |     number     |Set tamper (vibration) detection threshold. Lower value sets higher sensitivity. `1..127`, `0` - for disabled.|
|      `led_status_disable`      |      bool      |                              Disable LEDs on device if set. `true` or `false`.                               |
|           `schedule`           |      bool      |                  Enable or disable schedules and sunrise/sunset commands for this channel.                   |
|        `schedule_rules`        |array of strings|                            Rules for schedule activation, e.g. `0000-0123456-on`.                            |
|       `temp_over_value`        |     number     |                              Temperature over which to trigger `temp_over_url`.                              |
|       `temp_under_value`       |     number     |                             Temperature under which to trigger `temp_under_url`.                             |
|       `wifi_ap.enabled`        |      bool      |                                       Enable/Disable the device's AP.                                        |
|       `wifi_sta.enabled`       |      bool      |                                           Enable/Disable the WiFi.                                           |
|         `mqtt.enable`          |      bool      |                                             Enable/Disable MQTT.                                             |
|         `sntp.server`          |     string     |                                             Set the SNTP server.                                             |
|         `sntp.enabled`         |      bool      |                                             Enable/Disable SNTP.                                             |
|        `login.enabled`         |      bool      |                            Enable/Disable the requirement for login credentials.                             |
|      `login.unprotected`       |      bool      |                                      Enable/Disable unprotected login.                                       |
|        `login.username`        |     string     |                                              Set the username.                                               |
|    `login.default_username`    |     string     |                                          Set the default username.                                           |
|         `discoverable`         |      bool      |                                Set whether the device is discoverable or not.                                |
|        `cloud.enabled`         |      bool      |                                          Enable/Disable the Cloud.                                           |
|        `coiot.enabled`         |      bool      |                                            Enable/Disable CoIoT.                                             |
|     `coiot.update_period`      |     number     |                       Set the period of time in milliseconds before each CoIoT update.                       |
|           `timezone`           |     string     |                                          Set the device's timezone.                                          |
|        `tz_auto_detect`        |      bool      |                                  Enable/Disable autodetecting the timezone.                                  |
|        `tz_utc_offset`         |     number     |                              The offset from the UTC timezone in milliseconds.                               |
|   `sensors.temperature_unit`   |     string     |                                    `C` for Celsius or `F` for Fahrenheit.                                    |
|`sensors.temperature_threshohld`|     number     |                             Temperature delta (in °C), which triggers an update.                             |
|      `temperature_offset`      |     number     |                                   Temperature offset (in °C).`-50` - `+50`                                   |

Shelly Motion 2: `/settings/coiot`
----------

```
GET /settings/coiot

{
    "enabled": true
}

```

### Attributes ###

|Attribute|Type|      Description       |
|---------|----|------------------------|
|`enabled`|bool|Whether COIOT is enabled|

### Parameters ###

|  Parameter   | Type |    Description     |
|--------------|------|--------------------|
|`coiot_enable`| bool |Enable/Disable COIOT|
| `coiot_peer` |string|     COIOT peer     |

Shelly Motion 2: `/status`
----------

```
GET /status

{
    "wifi_sta": {
        "connected": true,
        "ssid": "topcho",
        "ip": "192.168.1.179",
        "rssi": -36
    },
    "cloud": {
        "enabled": false,
        "connected": false
    },
    "mqtt": {
        "connected": false
    },
    "time": "12:47",
    "unixtime": 1648205229,
    "serial": 0,
    "has_update": false,
    "mac": "84FD276ED988",
    "cfg_changed_cnt": 0,
    "actions_stats": {
        "skipped": 0
    },
    "sleep_time": 0,
    "lux": {
        "value": 16090,
        "illumination": "bright",
        "is_valid": true
    },
    "tmp": {
        "value": 999.0,
        "units": "C",
        "is_valid": true
    },
    "sensor": {
        "vibration": false,
        "motion": true,
        "timestamp": 1648205140,
        "active": true,
        "is_valid": true
    },
    "bat": {
        "value": 0,
        "voltage": 3.112
    },
    "charger": false,
    "update": {
        "status": "unknown",
        "has_update": false,
        "new_version": null,
        "old_version": "20220324-131952/master@383eea08+",
        "beta_version": null
    },
    "ram_total": 97280,
    "ram_free": 22928,
    "fs_size": 65536,
    "fs_free": 59540,
    "uptime": 76968,
    "fw_info": {
        "device": "shellymotion2-84FD276ED988",
        "fw": "20220324-131952/master@383eea08+"
    },
    "ps_mode": 0,
    "dbg_flags": 0
}

```

Sensor values are reported on the `/status` endpoint.

### Attributes ###

|    Attribute     | Type |                              Description                              |
|------------------|------|-----------------------------------------------------------------------|
|   `lux.value`    |number|              Illumination measure by the sensor in lux.               |
|`lux.illumination`|string|                 One of `dark`, `twilight`, `bright`.                  |
| `sensor.motion`  | bool |  Motion has been detected and the sensor blind time has not elapsed.  |
|`sensor.vibration`| bool |Tamper (vibration) has been detected. Cleared after vibration has gone.|
| `sensor.active`  | bool |                  Whether motion detection is active.                  |
|  `bat.voltage`   |number|                       Measured battery voltage.                       |
|   `bat.value`    |number|                      Battery charge in percent.                       |
|    `charger`     | bool |                     Whether a charger connected.                      |
|  `*.timestamp`   |number|                       Current device unix time.                       |
|   `*.is_valid`   | bool |                 Whether motion sensor self-checks OK.                 |

Shelly Motion 2: General HTTP Endpoints
----------

|    Endpoint     |                                               Description                                               |
|-----------------|---------------------------------------------------------------------------------------------------------|
|     `/pin`      |                                            Get/Generate pin.                                            |
|   `/selftest`   |                                     Check/Force factory self-test.                                      |
|     `/ota`      |                                     Check/Update firmware version.                                      |
|   `/poweroff`   |Requesting this endpoint will power off the device. It can be turned back on by pressing the user button.|
|    `/reboot`    |                                             Device reboot.                                              |
|  `/debug/log`   |                                          Shows the debug log.                                           |
|    `/psovrd`    |            Override powersave mode for the next 180 seconds and switch radio to full power.             |
|   `/psovrd2`    |      Override powersave mode for the next 180 seconds and set powersave mode to beacon skip to 10.      |
|`/cancel_psovrd` |                                       Cancel powersave override.                                        |
|`/settings/reset`|                                       Resets settings to default.                                       |
| `/settings/tz`  |                                      Does the same as `/settings`.                                      |

Shelly Motion 2: OTA update example
----------

`http://192.168.1.100/ota?url=http://shelly-api-eu.shelly.cloud/firmware/SHMOS-02_build.gbl`

Shelly TRV
==========

Shelly TRV: Overview
----------

Shelly TRV is a WiFi Smart thermostatic radiator valve with long battery life and constant connection to WiFi:

<https://shelly.cloud/shelly-thermostatic-radiator-valve/>

### Actions ###

Shelly TRV supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|   Action    |             Description             |
|-------------|-------------------------------------|
|`valve_close`|URL(s) to invoke when valve is closed|
|`valve_open` |URL(s) to invoke when valve is opened|

### Factory Reset ###

To restore Shelly TRV to its factory settings, turn the device on if needed, then press and hold the user button for \> 10 seconds. The device will reboot with the factory defaults into AP mode.

Shelly TRV: MQTT
----------

When configured for [MQTT](#mqtt-support), Shelly TRV sends values from its internal sensors on the following topics:

* `shellies/shellytrv-<id>/info`: publishes a JSON payload with the content of HTTP `/status` endpoint

### Command topics ###

Shelly TRV supports a set of commands published on `shellies/thermostat/0/command/` to address all TRVs or `shellies/shellytrv-<id>/thermostat/0/command/` to address an individual device:

* `settings` will trigger piblishing the content of http `/settings` endpoint

* `schedule` accepts `1` or `0` to enable/disable schedule

* `schedule_profile` accepts number from `1` to `5` to choose active schedule profile with the provided id

* `target_t` accepts number from `4` to `31` set target temperature.

* `ext_t` accepts number to send external sensor temperature, in `deg C`

* `valve_pos` accepts number from `0` to `100` to set manually the valve position, in `%`

* `boost_minutes` accepts number to start boost mode for the given minutes, in `minutes`

* `set_boost_minutes` accepts number to set the default boost time, in `minutes`

* `valve_min_percent` accepts number from `0` to `10` to set the valve clse postion percent, in `%`

* `accelerated_heating` accepts `1` or `0` to enable/disable accelerated heating

Shelly TRV: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly TRV SHTRV-01](docs/coiot/v2/examples/Shelly%20TRV%20SHTRV-01)

Shelly TRV: General HTTP Endpoints:
----------

|    Endpoint     |                                               Description                                               |
|-----------------|---------------------------------------------------------------------------------------------------------|
|     `/pin`      |                                            Get/Generate pin.                                            |
|   `/selftest`   |                                     Check/Force factory self-test.                                      |
|     `/ota`      |                                     Check/Update firmware version.                                      |
|   `/poweroff`   |Requesting this endpoint will power off the device. It can be turned back on by pressing the user button.|
|    `/reboot`    |                                             Device reboot.                                              |
|  `/calibrate`   |                                          Perform calibration.                                           |
|  `/debug/log`   |                                          Shows the debug log.                                           |
|    `/psovrd`    |            Override powersave mode for the next 180 seconds and switch radio to full power.             |
|   `/psovrd2`    |      Override powersave mode for the next 180 seconds and set powersave mode to beacon skip to 10.      |
|`/cancel_psovrd` |                                       Cancel powersave override.                                        |
|`/settings/reset`|                                       Resets settings to default.                                       |
| `/settings/tz`  |                                      Does the same as `/settings`.                                      |

Shelly TRV: `/settings`
----------

```
GET /settings

{
    "child_lock": false,
    "clog_prevention": false,
    "display": {
        "brightness": 7,
        "flipped": false
    },
    "thermostats": [
        {
            "target_t": {
                "enabled": true,
                "value": 31.0,
                "units": "C"
            },
            "schedule": false,
            "schedule_profile": 2,
            "schedule_profile_names": [
                "Livingroom",
                "Livingroom 1",
                "Bedroom",
                "Bedroom 1",
                "Holiday"
            ],
            "schedule_rules": [
                "0600-0123456-23",
                "0830-0123456-18",
                "1630-0123456-23",
                "2300-0123456-18"
            ],
            "temperature_offset": 0.0,
            "ext_t":{
                "enabled":false,
                "floor_heating": false},
            "t_auto":{
                "enabled":true},
            "boost_minutes":1000,
            "valve_min_percent":0.00,
            "force_close":false,
            "calibration_correction":true,
            "extra_pressure":false,
            "open_window_report":false}
        ]
}

```

### Attributes ###

|     Attribute      |     Type      |                                                   Description                                                    |
|--------------------|---------------|------------------------------------------------------------------------------------------------------------------|
|    `child_lock`    |     bool      |                        If set, the device stays in inactive state for the remaining time                         |
| `clog_prevention`  |     bool      |             If set, the device will move the piston in monday at 12:00 pm if not movemed for a week              |
|`display.brightness`|    number     |                                            Display brightness `1..7`                                             |
| `display.flipped`  |     bool      |                                            If the display is flipped                                             |
|   `thermostats`    |array of hashes|Thermostat settings. For detailed description, see [`/settings/thermostats/0`](#shelly-trv-settings-thermostats-0)|

### Parameters ###

|     Parameter      | Type |                        Description                        |
|--------------------|------|-----------------------------------------------------------|
|    `child_lock`    | bool |Set how long the device stays in inactive state, in seconds|
|`display_brightness`|number|              Set display brightness, `1..7`               |
| `display_flipped`  | bool |              Enable/disable flipped display               |

Shelly TRV: `/settings/thermostats/0`
----------

```
GET /settings/thermostats/0

{
    "target_t": {
        "enabled": true,
        "value": 31.0,
        "units": "C"
    },
    "schedule": false,
    "schedule_profile": 2,
    "schedule_profile_names": [
        "Livingroom",
        "Livingroom 1",
        "Bedroom",
        "Bedroom 1",
        "Holiday"
    ],
    "schedule_rules": [
        "0600-0123456-23",
        "0830-0123456-18",
        "1630-0123456-23",
        "2300-0123456-18"
    ],
    "temperature_offset": 0.0,
    "ext_t": {
        "enabled": false,
        "floor_heating": false
    },
    "t_auto": {
        "enabled": true
    },
    "boost_minutes": 30,
    "valve_min_percent": 0,
    "force_close": false,
    "calibration_correction": true,
    "extra_pressure": false,
    "open_window_report": false
}

```

### Attributes ###

|       Attribute        |      Type      |                                      Description                                      |
|------------------------|----------------|---------------------------------------------------------------------------------------|
|    `target_t.value`    |     number     |                              Target temperature `4..31`                               |
|   `target_t.enabled`   |      bool      |                       If the automatic valve control is enabled                       |
|    `target_t.units`    |     string     |                Units of the target temperature. Only `C` is supported                 |
|       `schedule`       |      bool      |                            If schedule is enabled/disabled                            |
|   `schedule_profile`   |     number     |             Choosen active schedule profile with the provided id, `1..5`              |
|`schedule_profile_names`|array of strings|                            List of schedule profiles names                            |
|    `schedule_rules`    |array of strings|                             Rules for schedule activation                             |
|  `temperature_offset`  |     number     |                              Temperature offset (in °C)                               |
|    `ext_t.enabled`     |      bool      |            If temperature correction from external temp sensor is enabled             |
| `ext_t.floor_heating`  |      bool      |               If enabled, only external tempreature sensor data is used               |
|    `t_auto.enabled`    |      bool      |                        Enables automatic temperature control.                         |
|    `boost_minutes`     |     number     |            Default boost time setting (100% open valve for the given time)            |
|     `min_percent`      |     number     |                    Set the valve closed position percent, `0..10`                     |
|     `force_close`      |      bool      |              Use extra pressure when fully closing the valve if enabled               |
|`calibration_correction`|      bool      |                     Use dynamic calibration correction if enabled                     |
|    `extra_pressure`    |      bool      |Use more force when moving the valve if enabled. The TRV can be more noisy in this mode|
|  `open_window_report`  |      bool      |                       Enable the open window mode of operation.                       |

### Parameters ###

|     Parameter      |      Type      |                                    Description                                    |
|--------------------|----------------|-----------------------------------------------------------------------------------|
|     `target_t`     |     number     |                            Target temperature `4..31`                             |
| `target_t_enabled` |      bool      |                     If the automatic valve control is enabled                     |
|  `target_t_units`  |     string     |              Units of the target temperature. Only `C` is supported               |
|     `schedule`     |      bool      |                          If schedule is enabled/disabled                          |
| `schedule_profile` |     number     |            Choose active schedule profile with the provided id, `1..5`            |
|   `profile_name`   |     string     |Name of the schedule profile. Should be used in combination with `schedule_profile`|
|  `schedule_rules`  |array of strings|                           Rules for schedule activation                           |
|`temperature_offset`|     number     |                            Temperature offset (in °C)                             |
|  `ext_t_enabled`   |      bool      |          Enable/disable temperature correction from external temp sensor          |

Shelly TRV: `/settings/coiot`
----------

```
GET /settings/coiot

{
    "enabled": true
}

```

### Attributes ###

|Attribute|Type|      Description       |
|---------|----|------------------------|
|`enabled`|bool|Whether COIOT is enabled|

### Parameters ###

|  Parameter   | Type |    Description     |
|--------------|------|--------------------|
|`coiot_enable`| bool |Enable/Disable COIOT|
| `coiot_peer` |string|     COIOT peer     |

Shelly TRV: `/status`
----------

```
GET /status

{
    "thermostats": [
        {
            "pos": -100.0,
            "target_t": {
                "enabled": true,
                "value": 31.0,
                "units": "C"
            },
            "tmp": {
                "value": 17.4,
                "units": "C",
                "is_valid": true
            },
            "schedule": false,
            "schedule_profile": 2
            "boost_minutes": 0
        }
    ],
    "calibrated": false,
    "bat": {
        "value": 0,
        "voltage": 3.127
    },
    "charger": false,
    "ps_mode": 0,
    "dbg_flags": 0
}

```

### Attributes ###

|  Parameter   |     Type      |                                                         Description                                                         |
|--------------|---------------|-----------------------------------------------------------------------------------------------------------------------------|
|`thermostats` |array of hashes|Contains the current state of the thermostat. See [`/thermostats/0`](#shelly-trv-thermostats-0) for description of attributes|
| `calibrated` |     bool      |                                               If the thermostat is calibrated                                               |
| `batt.value` |    number     |                                                  Battery charge in percent                                                  |
|`batt.voltage`|    number     |                                                  Measured battery voltage                                                   |
|  `charger`   |     bool      |                                               Whether a charger is connected                                                |

Shelly TRV: `/thermostats/0`
----------

```
GET /thermostats/0

{
    "pos": 23,
    "target_t": {
        "enabled": true,
        "value": 31.0,
        "units": "C"
    },
    "tmp": {
        "value": 17.4,
        "units": "C",
        "is_valid": true
    },
    "schedule": false,
    "schedule_profile": 2,
    "boost_minutes": 0,
    "window_open": false
}

```

### Attributes ###

|    Attribute     | Type |                                                               Description                                                                |
|------------------|------|------------------------------------------------------------------------------------------------------------------------------------------|
|      `pos`       |number|Position of the valve, `0..100` and `-1` if not calibrated. **Setting position to arbitrary value disables automatic temperature control**|
| `target_t.value` |number|                                                        Target temperature `4..31`                                                        |
|`target_t.enabled`| bool |                                                If the automatic valve control is enabled                                                 |
| `target_t_units` |string|                                          Units of the target temperature. Only `C` is supported                                          |
|   `tmp.value`    |number|                                                           Measured temperature                                                           |
|   `tmp.units`    | bool |                                         Units of the measured temperature. Only `C` is supported                                         |
|  `tmp.is_valid`  |string|                                           Whether the temperature sensor is operating properly                                           |
|    `schedule`    | bool |                                                     If schedule is enabled/disabled                                                      |
|`schedule_profile`|number|                                       Choosen active schedule profile with the provided id, `1..5`                                       |
| `boost_minutes`  |number|                                        Current active valve boost time counter (100% open state)                                         |
|  `window_open`   | bool |      Inform the TRV that a windows is open. If the open window report is enabled, the device will switch to the correspondig state       |

### Parameters ###

|   Parameter   | Type |                                       Description                                        |
|---------------|------|------------------------------------------------------------------------------------------|
|`boost_minutes`|number|Start boost operation for the desired minutes. Value of 0 stops the active boost operation|

Shelly TRV: `/window`
----------

### Attributes ###

|Attribute|Type|                            Description                             |
|---------|----|--------------------------------------------------------------------|
| `open`  |bool|Window is open or closed. Used only if open window report is enabled|

Shelly TRV: Window open example
----------

`http://192.168.1.100/window?state=open/close``http://192.168.1.100/window?state=true/false`

Shelly TRV: OTA update example
----------

`http://192.168.1.100/ota?url=http://shelly-api-eu.shelly.cloud/firmware/SHTRV-01_build.gbl`

Shelly4Pro
==========

Shelly4Pro: Overview
----------

Shelly4Pro is a 4-channel DIN mountable WiFi connected relay with power meters for each channel. With Shelly4Pro you can control 4 electrical circuits, 10 amperes each (4 x 2300 W). You can also monitor the real time consumption. Visit the product page for more information and to download the User Manual:

<https://shelly.cloud/products/shelly-4pro-smart-home-automation-relay/>

The operating mode of 4Pro can be set via the [`/settings`](#shelly4pro-settings) endpoint. Commands to perform actions can come from:

* A physical button
* HTTP request, trough the local web interface
* A command sent via the cloud
* A weekly-schedule event or a sunrise/sunset-generated event

### Factory Reset ###

If the web interface of the device cannot be accessed, settings can be brought back to defaults by pressing and holding the device button for more then 10 seconds or until the LED light start flashing fast.

### About the device ###

Each of the four channels is controlled individually and supports the **ON** and **OFF** commands. In this mode, an overpower threshold can be enabled for each of the channels, via the `max_power` parameter in [`/settings`](#shelly4pro-settings).

Relay channels also support `auto_on` and `auto_off` settings -- these are timers in seconds which will turn ON or OFF the channel when it has been turned OFF or ON respectively, from either a physical switch or network command. Thus, the user can set a limit for how long the channel can be **ON** or **OFF**.

Upon power-on, outputs are initialized using one of these strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly

Physical input switches can be one of:

* a momentary, push-button switch
* a toggle switch with two stable states
* an "edge" switch. In this input mode, every switch state transition causes a toggle of the output state. This can be used with input from existing two-way switch installations

**Note:** Setting output state based on inputs on power-on is not supported when inputs are configured as momentary or edge.

To control Shelly4Pro in **Relay** mode, use these resources:

* [`/settings/relay/{index}`](#shelly4pro-settings-relay-index) to configure the behavior of each channel
* [`/relay/{index}`](#shelly4pro-relay-index) to control and monitor the channel

Shelly4Pro: MQTT
----------

Shelly 4Pro uses the following topics for each channel. `<i>` ranges from 0 to 3:

* `shellies/shelly4pro-<deviceid>/input/<i>` reports the current state as `0` or `1`
* `shellies/shelly4pro-<deviceid>/relay/<i>` to report status: `on`, `off` or `overpower`
* `shellies/shelly4pro-<deviceid>/relay/<i>/power` to report instantaneous power consumption rate in Watts
* `shellies/shelly4pro-<deviceid>/relay/<i>/energy` to report amount of energy consumed in Watt-minute
* `shellies/shelly4pro-<deviceid>/relay/<i>/command` accepts `on`, `off` or `toggle` and applies accordingly

Shelly4Pro: `/settings`
----------

```
GET /settings

{
    "relays": [
        {
            "name": null,
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "off",
            "btn_type": "toggle",
            "auto_on": 0,
            "auto_off": 0,
            "max_power": 0,
            "schedule": true,
            "schedule_rules": []
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ]
}

```

Shelly4Pro extends the common `/settings` endpoint with relay and power consumption status and contains the settings for this device's **Relays** . They are indexed, to allow implementation of the same interface on devices with more output channels.

Shelly4Pro also exposes [`/settings/relay/{index}`](#shelly4pro-settings-relay-index) for setting the channel parameters.

### Attributes ###

|Attribute|     Type      |                                        Description                                        |
|---------|---------------|-------------------------------------------------------------------------------------------|
|`relays` |array of hashes|See [`/settings/relay/{index}`](#shelly4pro-settings-relay-index) for explanation of values|
|`meters` |array of hashes|         Contains the status of the integrated power meter, see description below          |

### `meters` attributes ###

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|            Energy counter value for the last 3 round minutes            |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

The `counters` array contains the values of the energy counter per channel for the last 3 round minutes. The value will always increase, but will reset to zero on reboot or power cycle. When observing this value (over MQTT or HTTP polling) the observer should keep an accumulator locally, and add the new value whenever it goes backwards.

Shelly4Pro: `/settings/relay/{index}`
----------

```
GET /settings/relay/0

{
    "name": null,
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "btn_type": "toggle",
    "auto_on": 0,
    "auto_off": 0,
    "max_power": 0,
    "schedule": true,
    "schedule_rules": []
}

```

The returned document here is identical to the data returned in `/settings` for the particular output channel in the `relays` array. The attributes match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                                 Description                                 |
|----------------|----------------|-----------------------------------------------------------------------------|
|     `name`     |     string     |                                 Relay name                                  |
|     `ison`     |      bool      |                                Channel state                                |
|  `has_timer`   |      bool      |               Whether there is an active timer on the channel               |
|  `overpower`   |      bool      |                 Whether an overpower condition has occurred                 |
|`default_state` |     string     |        Power-on default state, one of `off`, `on`, `last`, `switch`         |
|   `btn_type`   |     string     |   Button type, one of `momentary`, `toggle`, `edge`, `action`, `detached`   |
|   `auto_on`    |     number     |Automatic flip back timer, seconds. Will engage after turning the channel OFF|
|   `auto_off`   |     number     |Automatic flip back timer, seconds. Will engage after turning the channel ON |
|  `max_power`   |     number     |                       Per-channel overpower threshold                       |
|   `schedule`   |      bool      |                        Whether scheduling is enabled                        |
|`schedule_rules`|array of strings|                        Rules for schedule activation                        |

### Parameters ###

|   Parameter    |      Type      |                                           Description                                            |
|----------------|----------------|--------------------------------------------------------------------------------------------------|
|    `reset`     |      any       |Submitting a non-empty value will reset settings for this relay output channel to factory defaults|
|     `name`     |     string     |                                            Relay name                                            |
|`default_state` |     string     |                          Accepted values: `off`, `on`, `last`, `switch`                          |
|   `btn_type`   |     string     |               Accepted values: `momentary`, `toggle`, `edge`, `action`, `detached`               |
|   `auto_on`    |     number     |          Automatic flip back timer, seconds. Will engage after turning the channel OFF           |
|   `auto_off`   |     number     |           Automatic flip back timer, seconds. Will engage after turning the channel ON           |
|  `max_power`   |     number     |                                 Per-channel overpower threshold                                  |
|   `schedule`   |      bool      |                                   Enable or disable schedules                                    |
|`schedule_rules`|array of strings|                      Rules for schedule activation, e.g. `0000-0123456-on`                       |

Shelly4Pro: `/status`
----------

```
GET /status

{
    "relays": [
        {
            "ison": false,
            "has_timer": false,
            "timer_remaining": 0,
            "overpower": false,
            "is_valid": true
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ]
}

```

4Pro adds information about the current state of the output channels and power metering.

### Attributes ###

|Attribute|     Type      |                                                             Description                                                              |
|---------|---------------|--------------------------------------------------------------------------------------------------------------------------------------|
|`relays` |array of hashes|Contains the current state of the relay output channels. See [`/relay/{index}`](#shelly4pro-relay-index) for description of attributes|
|`meters` |array of hashes|                      Current status of the power meters, see description in [`/settings`](#shelly4pro-settings)                      |

Shelly4Pro: `/meter/{index}`
----------

```
GET /meter/0

{
    "power": 0,
    "is_valid": true,
    "timestamp": 0,
    "counters": [1,2,3],
    "total": 4
}

```

### Attributes ###

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|    Energy counter value for the last 3 round minutes in Watt-minute     |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

Shelly4Pro: `/relay/{index}`
----------

```
GET /relay/0

{
    "ison": false,
    "has_timer": false,
    "timer_remaining": 0,
    "overpower": false,
    "is_valid": true
}

```

Shows current status of each output channel and accepts commands for controlling the channel via [`/settings`](#shelly4pro-settings).

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                    Whether an overpower condition turned the channel OFF                     |
|   `is_valid`    | bool |                 Whether the associated power meter is functioning correctly                  |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly Plug / PlugS
==========

Shelly Plug/PlugS: Overview
----------

Shelly Plug/PlugS are among the most intelligent Wi-Fi power outlets on the market today. Visit the product pages for a detailed features overview and User Manual:

<https://shelly.cloud/products/shelly-plug-smart-home-automation-device/>

<https://shelly.cloud/products/shelly-plug-s-smart-home-automation-device/>

The settings of Shelly Plug can be changed via the [`/settings`](#shelly-plug-plugs-settings) endpoint. Commands to perform actions can come from:

* A physical button
* HTTP request, trough the local web interface
* A command sent via the cloud
* A weekly-schedule event or a sunrise/sunset-generated event

Shelly Plug/PlugS supports up to 20 schedule rules.

### Factory Reset ###

If the web interface of the device cannot be accessed, settings can be brought back to defaults by holding the button for more than 10 seconds or until the red LED starts flashing rapidly.

### About the device ###

Shelly Plug supports the **ON** and **OFF** commands. An overpower threshold can be enabled, via the `max_power` parameter in [`/settings`](#shelly-plug-plugs-settings). If set to a value different than 0, the relay will automatically turn off if current power consumption exceeds the value of `max_power`.

Shelly Plug also support `auto_on` and `auto_off` settings -- these are timers in seconds which will turn ON or OFF the plug when it has been turned OFF or ON respectively. Thus, the user can set a limit for how long the plug can be **ON** or **OFF**.

Upon power-on, output is initialized using one of 4 available strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly

To control Shelly Plug/PlugS, use these resources:

* [`/settings/relay/0`](#shelly-plug-plugs-settings-relay-0) to configure the behavior of the plug
* [`/relay/0`](#shelly-plug-plugs-settings-relay-0) to control and monitor the plug

Shelly Plug/PlugS: MQTT
----------

MQTT topics used by Plug / PlugS (where `<model>` is either `shellyplug` or `shellyplug-s`):

* `shellies/<model>-<deviceid>/relay/0` to report status: `on`, `off` or `overpower`
* `shellies/<model>-<deviceid>/relay/0/power` to report instantaneous power consumption rate in Watts
* `shellies/<model>-<deviceid>/relay/0/energy` to report amount of energy consumed in Watt-minute
* `shellies/<model>-<deviceid>/relay/0/overpower_value` reports the value in Watts, on which an overpower condition is detected
* `shellies/<model>-<deviceid>/relay/0/command` accepts `on`, `off` or `toggle` and applies accordingly

Shelly PlugS adds:

* `shellies/shellyplug-s-<deviceid>/temperature` reports internal device temperature in °C
* `shellies/shellyplug-s-<deviceid>/temperature_f` reports internal device temperature in °F
* `shellies/shellyplug-s-<deviceid>/overtemperature` reports `1` when device has overheated, normally `0`

Shelly Plug/PlugS: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Plug E SHPLG2-1](docs/coiot/v2/examples/Shelly%20Plug%20E%20SHPLG2-1)
* [Shelly Plug SHPLG-1](docs/coiot/v2/examples/Shelly%20Plug%20SHPLG-1)
* [Shelly Plug S SHPLG-S](docs/coiot/v2/examples/Shelly%20Plug%20S%20SHPLG-S)
* [Shelly Plug US SHPLG-U1](docs/coiot/v2/examples/Shelly%20Plug%20US%20SHPLG-U1)

Shelly Plug/PlugS: `/settings`
----------

Shelly Plug extends the common `/settings` endpoint with power consumption status and contains the settings for this device.

```
GET /settings (Shelly PlugS)

{
    "max_power": 3500,
    "led_power_disable": false,
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "out_on_url",
            "out_off_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "appliance_type": "General",
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "off",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": [],
            "max_power": 0
        }
    ]
}

```

Shelly Plug adds `max_power` to the list of parameters which can be set via
the common `/settings` endpoint:

### Attributes ###

|     Attribute     |     Type      |                                                             Description                                                              |
|-------------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------|
|    `max_power`    |    number     |                                                     Overpower threshold in Watts                                                     |
|`led_power_disable`|     bool      |                                  **PlugS only** Whether LED indication for output status is enabled                                  |
|     `actions`     |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-plug-plugs-settings-actions)|
|     `relays`      |array of hashes|                       See [`/settings/relay/0`](#shelly-plug-plugs-settings-relay-0) for explanation of values                       |

### Parameters ###

|     Parameter     | Type |                                    Description                                    |
|-------------------|------|-----------------------------------------------------------------------------------|
|    `max_power`    |number|                           Overpower threshold in Watts                            |
|`led_power_disable`| bool |              **PlugS only** Disable LED indication for output status              |
|     `actions`     | hash |For setting actions, see [`/settings/actions`](#shelly-plug-plugs-settings-actions)|

Shelly Plug/PlugS: `/settings/actions`
----------

```

GET /settings/actions
{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Plug/PlugS supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|   Action    |Index|              Description               |
|-------------|-----|----------------------------------------|
|btn\_on\_url |  0  |URL to access when SW input is activated|
|out\_on\_url |  0  | URL to access when output is activated |
|out\_off\_url|  0  |URL to access when output is deactivated|

Shelly Plug/PlugS: `/settings/relay/0`
----------

```
GET /settings/relay/0

{
    "name": null,
    "appliance_type": "General",
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": [],
    "max_power": 0
}

```

The returned document here is identical to the data returned in `/settings` for the single output channel in the `relays` array. The channel index exists to preserve API compatibility with multi-channel Shelly devices. Attributes in the response match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                               Description                                |
|----------------|----------------|--------------------------------------------------------------------------|
|     `name`     |     string     |                                Relay name                                |
|`appliance_type`|     string     |                    Custom configurable appliance type                    |
|     `ison`     |      bool      |                           State of the channel                           |
|  `has_timer`   |      bool      |             Whether there is an active timer on the channel              |
|  `overpower`   |      bool      |               Whether an overpower condition has occurred                |
|`default_state` |     string     |            Default power-on state, one of `off`, `on`, `last`            |
|   `auto_on`    |     number     |Automatic flip back timer, seconds. Will engage after turning the plug OFF|
|   `auto_off`   |     number     |Automatic flip back timer, seconds. Will engage after turning the plug ON |
|   `schedule`   |      bool      |                      Whether scheduling is enabled                       |
|`schedule_rules`|array of strings|                      Rules for schedule activation                       |
|  `max_power`   |     number     |                       Overpower threshold in Watts                       |

### Parameters ###

|   Parameter    |      Type      |                                      Description                                       |
|----------------|----------------|----------------------------------------------------------------------------------------|
|     `name`     |     string     |                                     Set relay name                                     |
|`appliance_type`|     string     |                         Set custom configurable appliance type                         |
|    `reset`     |      any       |Submitting a non-empty value will reset settings for the plug output to factory defaults|
|`default_state` |     string     |                          Accepted values: `off`, `on`, `last`                          |
|   `auto_on`    |     number     |       Automatic flip back timer, seconds. Will engage after turning the plug OFF       |
|   `auto_off`   |     number     |       Automatic flip back timer, seconds. Will engage after turning the plug ON        |
|   `schedule`   |      bool      |                                 Enable schedule timer                                  |
|`schedule_rules`|array of strings|                 Rules for schedule activation, e.g. `0000-0123456-on`                  |
|  `max_power`   |     number     |                              Overpower threshold in Watts                              |

Shelly Plug/PlugS: `/status`
----------

```
GET /status (Shelly PlugS)

{
    "relays": [
        {
            "ison": true,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "source": "http"
        }
    ],
    "meters": [
        {
            "power": 0.01,
            "overpower": 23.78,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ],
    "temperature": 41.94,
    "overtemperature": false,
    "tmp": {
        "tC": 41.94,
        "tF": 107.5,
        "is_valid": true
    }
}

```

Shelly Plug adds information about the current state of the plug (ON or OFF) and instantaneous power reading in Watts.

### Attributes ###

|    Attribute    |     Type      |                                                            Description                                                            |
|-----------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------|
|    `relays`     |array of hashes|Contains the current state of the relay output channels. See [`/relay/0`](#shelly-plug-plugs-relay-0) for description of attributes|
|    `meters`     |array of hashes|                                                 Current status of the power meter                                                 |
|  `temperature`  |    number     |                                         **PlugS only** internal device temperature in °C                                          |
|`overtemperature`|     bool      |                                         **PlugS only** `true` when device has overheated                                          |
|    `tmp.tC`     |    number     |                                         **PlugS only** Internal device temperature in °C                                          |
|    `tmp.tF`     |    number     |                                         **PlugS only** Internal device temperature in °F                                          |
| `tmp.is_valid`  |     bool      |                            **PlugS only** Whether the internal temperature sensor functions correctly                             |

Shelly Plug/PlugS: `/meter/0`
----------

```
GET /meter/0

{
    "power": 0,
    "overpower": 23.78,
    "is_valid": true,
    "timestamp": 0,
    "counters": [1,2,3],
    "total": 4
}

```

### Attributes ###

| Attribute |      Type      |                               Description                               |
|-----------|----------------|-------------------------------------------------------------------------|
|  `power`  |     number     |               Current real AC power being drawn, in Watts               |
|`is_valid` |      bool      |                  Whether power metering self-checks OK                  |
|`overpower`|     number     |       Value in Watts, on which an overpower condition is detected       |
|`timestamp`|     number     |  Timestamp of the last energy counter value, with the applied timezone  |
|`counters` |array of numbers|    Energy counter value for the last 3 round minutes in Watt-minute     |
|  `total`  |     number     |Total energy consumed by the attached electrical appliance in Watt-minute|

Shelly Plug/PlugS: `/relay/0`
----------

```
GET /relay/0

{
    "ison": false,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "source": "http"
}

```

Shows current status of the output channel and accepts commands for controlling the channel.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                    Whether an overpower condition turned the channel OFF                     |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly i3
==========

Shelly i3: Overview
----------

Shelly i3 is a WiFi AC switch reader. It has 3 independent input channels which can operare with all types of toggle and momentary AC switches.

Shelly i3 can detect and announce not only simple ON/OFF state changes, but also complex (multipush) input events, for example double shortpush, shortpush + longpush, etc. For each of this events Shelly i3 can invoke user-configurable action URLs. For more information see [Shelly i3: Input events](#shelly-i3-input-events)

The [product page](https://shelly.cloud/products/shelly-i3-smart-home-automation-device/) has all key features described, wiring diagram and User Manual.

### Factory Reset ###

To perform a factory reset on a Shelly i3 device:

* hold the user button for 5 seconds to reset WiFi to AP mode
* hold the user button for 10 seconds to perform a complete factory reset
* flip an input switch quickly 5 times within the first minute after power-on to perform a complete factory reset

Shelly i3: Input events
----------

Shelly i3 can detect and announce the following input events on any of its channels:

* **Shortpush**
* **Longpush**
* **Double shortpush**
* **Triple shortpush**
* **Shortpush + longpush**
* **Longpush + shortpush**

For each input event, an action URL can be configured via the [`/settings/input/{index}`](#shelly-i3-settings-input-index) endpoint.

To configure the detection of input events, set the parameters described below via the [`/settings`](#shelly-i3-settings) endpoint.
These parameters are common for all 3 input channels.

|              Parameter               | Type |             Accepted values              |Default |
|--------------------------------------|------|------------------------------------------|--------|
|      `longpush_duration_ms_min`      |number|               \>= `100ms`                |`800ms` |
|      `longpush_duration_ms_max`      |number|\>= (`longpush_duration_ms_min` + `100ms`)|`3000ms`|
|`multipush_time_between_pushes_ms_max`|number|               \>= `100ms`                |`500ms` |

Following rules apply:

* Input events events are only monitored if a button is configured as `momentary`
* Button pushes shorter than `longpush_duration_ms_min` are interpreted as **shortpush**
* Button pushes between `longpush_duration_ms_min` and `longpush_duration_ms_max` are interpreted as **longpush**
* A sequence of button pushes is interpreted as a single event only if the time between them doesn't exceed `multipush_time_between_pushes_ms_max`.
  For example, if the time between two shortpushes is less than `multipush_time_between_pushes_ms_max`, Shelly i3 will announce a **double shortpush** event. If the time between the pushes is greater than `multipush_time_between_pushes_ms_max`, Shelly i3 will announce two separate **shortpush** events one after the other.

Shelly i3 announces input events using the attributes described below (see [`/status`](#shelly-i3-status)):

| Attribute | Type |           Value           |Value on power-on / reboot|
|-----------|------|---------------------------|--------------------------|
|  `event`  |string|   `""` = none / invalid   |           `""`           |
|           |      |      `S` = shortpush      |                          |
|           |      |      `L` = longpush       |                          |
|           |      |  `SS` = double shortpush  |                          |
|           |      | `SSS` = triple shortpush  |                          |
|           |      |`SL` = shortpush + longpush|                          |
|           |      |`LS` = longpush + shortpush|                          |
|`event_cnt`|number|         `uint16`          |           `0`            |

The event counter `event_cnt` is incremented each time there is a new `event` on the input channel. It doesn't take in account which event it is exactly. On power-on / reboot, the value of the counter is 0.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Shelly i3: MQTT
----------

Shelly i3 publishes on the following MQTT topics, where `<index>` is the input channel (0,1,2):

|                    MQTT topic                     |                                               Message                                               |Message on power-on / reboot|
|---------------------------------------------------|-----------------------------------------------------------------------------------------------------|----------------------------|
|   `shellies/shellyix3-<deviceid>/input/<index>`   |                                         `0` = input is OFF                                          | depends on physical state  |
|                                                   |                                          `1` = input is ON                                          |                            |
|`shellies/shellyix3-<deviceid>/input_event/<index>`|                               `{"event":"string","event_cnt":number}`                               |`{"event":"","event_cnt":0}`|
|                                                   |`event` and `event_cnt` are described in detail in [Shelly i3: Input events](#shelly-i3-input-events)|                            |
|`shellies/shellyix3-<deviceid>/temperature_status` |                                    `Normal`, `High`, `Very High`                                    | depends on physical state  |

**Note**: by default, Shelly i3 will send periodic MQTT updates every 30 seconds. You can turn these off and only receive messages when an input has changed by setting the `mqtt_update_period` parameter to 0 (see [`/settings`](#settings)).

Shelly i3: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly i3 SHIX3-1](docs/coiot/v2/examples/Shelly%20i3%20SHIX3-1)

Shelly i3: `/settings`
----------

```
GET /settings

{
    "longpush_duration_ms": {
        "min": 800,
        "max": 3000
    },
    "multipush_time_between_pushes_ms": {
        "max": 500
    },
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "btn_off_url",
            "shortpush_url",
            "longpush_url",
            "double_shortpush_url",
            "triple_shortpush_url",
            "shortpush_longpush_url",
            "longpush_shortpush_url"
        ]
    },
    "inputs": [
        {
            "name": null,
            "btn_type": "momentary",
            "btn_reverse": 0,
        },
        {
            "name": null,
            "btn_type": "momentary",
            "btn_reverse": 0,
        },
        {
            "name": null,
            "btn_type": "momentary",
            "btn_reverse": 0,
        }
    ],
    "led_status_disable": false
}

```

Shelly i3 extends the common [`/settings`](#settings) endpoint with input timing settings and adds [`/settings/input/{index}`](#shelly-i3-settings-input-index) for configuring input channel-specific parameters.

### Attributes ###

|              Attribute               |     Type      |                                                         Description                                                          |
|--------------------------------------|---------------|------------------------------------------------------------------------------------------------------------------------------|
|         `led_status_disable`         |     bool      |                                           Whether LED status indication is enabled                                           |
|      `longpush_duration_ms.min`      |    number     |                                                  Longpush min duration (ms)                                                  |
|      `longpush_duration_ms.max`      |    number     |                                                  Longpush max duration (ms)                                                  |
|`multipush_time_between_pushes_ms.max`|    number     |                                           Max time between sequential pushes (ms)                                            |
|              `actions`               |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-i3-settings-actions)|
|               `inputs`               |array of hashes|                               See [`/settings/input/{index}`](#shelly-i3-settings-input-index)                               |

### Parameters ###

For a detailed description see [Shelly i3: Input events](#shelly-i3-input-events)

|              Parameter               | Type |                                Description                                |
|--------------------------------------|------|---------------------------------------------------------------------------|
|         `led_status_disable`         | bool |                       Disable LED status indication                       |
|      `longpush_duration_ms_min`      |number|                      Set longpush min duration (ms)                       |
|      `longpush_duration_ms_max`      |number|                      Set longpush max duration (ms)                       |
|`multipush_time_between_pushes_ms_max`|number|                Set max time between sequential pushes (ms)                |
|              `actions`               | hash |For setting actions, see [`/settings/actions`](#shelly-i3-settings-actions)|

Shelly i3: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "double_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "triple_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    ...
    ...
  }
}

```

### Actions ###

Shelly i3 supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|         Action         |Index|                                       Description                                        |
|------------------------|-----|------------------------------------------------------------------------------------------|
|      `btn_on_url`      | 0-2 |          URL to access when switch is ON (works only when `btn_type`=`toggle`)           |
|     `btn_off_url`      | 0-2 |          URL to access when switch is OFF (works only when `btn_type`=`toggle`)          |
|    `shortpush_url`     | 0-2 |   URL to access when switch is pressed short (works only when `btn_type`=`momentary`)    |
|     `longpush_url`     | 0-2 |    URL to access when switch is pressed long (works only when `btn_type`=`momentary`)    |
| `double_shortpush_url` | 0-2 |  URL to access when switch is 2x pressed short (works only when `btn_type`=`momentary`)  |
| `triple_shortpush_url` | 0-2 |  URL to access when switch is 3x pressed short (works only when `btn_type`=`momentary`)  |
|`shortpush_longpush_url`| 0-2 |URL to access when switch is pressed short + long (works only when `btn_type`=`momentary`)|
|`longpush_shortpush_url`| 0-2 |URL to access when switch is pressed long + short (works only when `btn_type`=`momentary`)|

Shelly i3: `/settings/input/{index}`
----------

```
GET /settings/input/0

{
    "name": null,
    "btn_type": "momentary",
    "btn_reverse": 0,
}

```

The returned document here is identical to the data returned in [`/settings`](#shelly-i3-settings) for the particular input channel in the `inputs` array.

### Attributes ###

|  Attribute  | Type |            Description             |
|-------------|------|------------------------------------|
|   `name`    |string|             Input name             |
| `btn_type`  |string|Button type: `toggle` or `momentary`|
|`btn_reverse`|number| If input logical state is inverted |

### Parameters ###

|  Parameter  | Type |                                        Description                                        |
|-------------|------|-------------------------------------------------------------------------------------------|
|   `reset`   | any  |Submitting a non-empty value will reset settings for this input channel to factory defaults|
|   `name`    |string|                                      Set input name                                       |
| `btn_type`  |string|                         Set button type: `toggle` or `momentary`                          |
|`btn_reverse`| bool |                       Set whether to invert the input logical state                       |

Shelly i3: `/status`
----------

```
GET /status

{
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 11,
            "last_sequence": "S"
        },
        {
            "input": 1,
            "event": "",
            "event_cnt": 22,
            "last_sequence": "SS"
        },
        {
            "input": 2,
            "event": "",
            "event_cnt": 15,
            "last_sequence": "LS"
        }
    ],
    "temperature_status": "Normal"
}

```

Shelly i3 extends the common [`/status`](#status) endpoint with the current status of the input channels.

### Attributes ###

|     Attribute      |     Type      |                                                         Description                                                          |
|--------------------|---------------|------------------------------------------------------------------------------------------------------------------------------|
|      `inputs`      |array of hashes|Contains the current state of the input channels. See [`/input/{index}`](#shelly-i3-input-index) for description of attributes|
|`temperature_status`|    string     |                              Temperature status of the device, "Normal", "High" or "Very High"                               |

Shelly i3: `/input/{index}`
----------

```
GET /input/0

{
    "input": 0,
    "event": "S",
    "event_cnt": 11,
    "last_sequence": "S"
}

```

Shows current status of `{index}` input channel.

### Attributes ###

|   Attribute   | Type |                                   Description                                    |
|---------------|------|----------------------------------------------------------------------------------|
|    `input`    |number|                                `0` = input is OFF                                |
|               |      |                                `1` = input is ON                                 |
|    `event`    |string|       Input event, see [Shelly i3: Input events](#shelly-i3-input-events)        |
|  `event_cnt`  |number|   Input event counter, see [Shelly i3: Input events](#shelly-i3-input-events)    |
|`last_sequence`|string|Last triggered input event, see [Shelly i3: Input events](#shelly-i3-input-events)|

Shelly Button1
==========

Shelly Button1: Overview
----------

Shelly Button1 is a WiFi button which can detect and announce 4 types of button presses - short, 2x short, 3x short, long. We developed Shelly Button1 to help you easily activate or deactivate any device or scene manually with just a click. Powered by rechargeable batteries, allowing for more than 3000 actions per charge. As an option it can be connectted via USB for constant power supply and Wi-Fi connection. Response time of less than 2sec. on battery and 100 ms on USB power.

The [product page](https://shelly.cloud/products/shelly-button-1-smart-home-automation-device/) has all key features described and User Manual.

### Factory Reset ###

To perform a factory reset on a Shelly Button1:

* you will need to remove the back cover of the device. The reset button is below the battery. Carefully move the battery and hold the reset button for 10 seconds.

Shelly Button1: MQTT
----------

Shelly Button1 publishes on the following MQTT topics:

* `shellies/shellybutton1-<deviceid>/sensor/battery`: battery level in %
* `shellies/shellybutton1-<deviceid>/input_event/0`: reports input event and event counter, e.g. `{"event":"S","event_cnt":2}` see [`/input/0`](#shelly-button1-input-0) for details

Shelly Button1: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Button SHBTN-1](docs/coiot/v2/examples/Shelly%20Button%20SHBTN-1)

Shelly Button1: `/settings`
----------

```
GET /settings

{
    "device": {
        "sleep_mode": true
    },
    "sleep_mode": {
        "period": 12,
        "unit": "h"
    },
    "led_status_disable": false,
    "longpush_duration_ms": {
        "max": 800
    },
    "multipush_time_between_pushes_ms": {
        "max": 500
    },
    "remain_awake": 0,
    "actions": {
        "active": false,
        "names": [
            "shortpush_url",
            "double_shortpush_url",
            "triple_shortpush_url",
            "longpush_url"
        ]
    },
    "inputs": [
        {
            "name": null
        }
    ]
}

```

### Attributes ###

|              Attribute               |     Type      |                                                            Description                                                            |
|--------------------------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------|
|         `device.sleep_mode`          |     bool      |                                                           Always `true`                                                           |
|         `sleep_mode.period`          |    number     |                                                Periodic update period, always `12`                                                |
|          `sleep_mode.unit`           |    string     |                                                            Always `h`                                                             |
|         `led_status_disable`         |     bool      |                                              Whether status LED is enabled/disabled                                               |
|      `longpush_duration_ms.max`      |    number     |                                                    Longpush max duration (ms)                                                     |
|`multipush_time_between_pushes_ms.max`|    number     |                                              Max time between sequential pushes (ms)                                              |
|            `remain_awake`            |    number     |                                          Time after last event before go to sleep in sec                                          |
|              `actions`               |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-button1-settings-actions)|
|               `inputs`               |array of hashes|                                    See [`/settings/input/0`](#shelly-button1-settings-input-0)                                    |

### Parameters ###

|              Parameter               | Type |                                  Description                                   |
|--------------------------------------|------|--------------------------------------------------------------------------------|
|            `remain_awake`            |number|         Set time after last event before go to sleep in sec, `[0..5]`          |
|      `longpush_duration_ms_max`      |number|                 Set longpush max duration (ms), `[800..2000]`                  |
|`multipush_time_between_pushes_ms_max`|number|           Set max time between sequential pushes (ms), `[200..2000]`           |
|              `actions`               | hash |For setting actions, see [`/settings/actions`](#shelly-button1-settings-actions)|
|         `led_status_disable`         | bool |                           Enable/disable status LED                            |

Shelly Button1: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "double_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "triple_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Button1 supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|        Action        |Index|                 Description                 |
|----------------------|-----|---------------------------------------------|
|   `shortpush_url`    |  0  | URL to access when switch is pressed short  |
|`double_shortpush_url`|  0  |URL to access when switch is 2x pressed short|
|`triple_shortpush_url`|  0  |URL to access when switch is 3x pressed short|
|    `longpush_url`    |  0  |  URL to access when switch is pressed long  |

Shelly Button1: `/settings/input/0`
----------

```
GET /settings/input/0

{
    "name": null,
}

```

### Attributes ###

|Attribute| Type |Description|
|---------|------|-----------|
| `name`  |string|Input name |

### Parameters ###

|Parameter| Type | Description  |
|---------|------|--------------|
| `name`  |string|Set input name|

Shelly Button1: `/status`
----------

```
GET /status

{
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 11
        }
    ],
    "is_valid": true,
    "bat": {
        "value": 71,
        "voltage": 2.73
    },
    "charger": false,
    "act_reasons": [
        "button"
    ],
    "connect_retries": 0
}

```

### Attributes ###

|    Attribute    |      Type      |                                                       Description                                                       |
|-----------------|----------------|-------------------------------------------------------------------------------------------------------------------------|
|    `inputs`     |array of hashes |Contains the current state of the input channels. See [`/input/0`](#shelly-button1-input-0) for description of attributes|
|   `is_valid`    |      bool      |                                              Whether button self-checks OK                                              |
|   `bat.value`   |     number     |                                   Estimated remaining battery capacity in %, `0..100`                                   |
|  `bat.voltage`  |     number     |                                                  Battery voltage, `V`                                                   |
|    `charger`    |      bool      |                                           Whether external power is available                                           |
|  `act_reasons`  |array of strings|       List of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `ext_power`       |
|`connect_retries`|     number     |                                                  WiFi connect retries                                                   |
| `sensor_error`  |     number     |                                             Only displayed in case of error                                             |

Shelly Button1: `/input/0`
----------

```
GET /input/0

{
    "input": 0,
    "event": "S",
    "event_cnt": 11
}

```

### Attributes ###

| Attribute | Type |                                          Description                                          |
|-----------|------|-----------------------------------------------------------------------------------------------|
|  `input`  |number|                               Input state physical - always `0`                               |
|  `event`  |string|Input event, `S` = shortpush, `SS` = double shortpush, `SSS` = triple shortpush, `L` = longpush|
|`event_cnt`|number|         Input event counter, `uint32`, stored in RTC memory when device goes to sleep         |

Shelly Bulb
==========

Shelly Bulb: Overview
----------

**Shelly Bulb** is a WiFi-enabled E27 bulb with Red, Green, Blue and White LEDs. Visit the product page for detailed information and User Manual:

<https://shelly.cloud/products/shelly-bulb-smart-home-automation-device/>

A number of exposed endpoints allow configuring all aspects of Shelly Bulb:

* controlling device configuration including WiFi mode and device mode and device-specific options
* controlling brightness and color of the bulb

Shelly Bulb supports up to 20 schedule rules.

### Factory Reset ###

Factory reset can be performed by:

* powering the device ON and then OFF 5 times in a row in 5-second intervals
* via the web interface of the device

Performing factory reset will revert all settings to their initial values.

Shelly Bulb: Device Modes
----------

Shelly Color can operate in two distinct device modes:

* **Color**
* **Warm/Cold White**

In **Color** mode, each output channel: Red, Green, Blue and White is individually controllable.

In **Warm/Cold White** mode the device accepts color temperature and brightness and adjusts power output of all channels to produce the desired white light.

Shelly Bulb can also play a set of pre-defined effects, specified by a numerical index:

* `0` - Off
* `1` - Meteor Shower
* `2` - Gradual Change
* `3` - Flash
* `4` - Breath
* `5` - On/Off Gradual
* `6` - Red/Green Change

Shelly Bulb: MQTT
----------

Shelly Bulb allows the simple `on` and `off` commands, as well as setting the color, brightness and effects using a JSON payload.

To control the bulb with a simple on-off switch functionality, use:

* `shellies/shellybulb-<deviceid>/color/0/command` accepts `on` and `off` payloads
* `shellies/shellybulb-<deviceid>/color/0` is used by the device to report its current on-off state

For controlling other parameters of the LED channels publish to:

* `shellies/shellybulb-<deviceid>/color/0/set`

The device expects a JSON payload on this topic, with the following sample contents:

```
{
    "mode": "color",    /* "color" or "white" */
    "red": 0,           /* red brightness, 0..255, applies in mode="color" */
    "green": 0,         /* green brightness, 0..255, applies in mode="color" */
    "blue": 255,        /* blue brightness, 0..255, applies in mode="color" */
    "gain": 100,        /* gain for all channels, 0..100, applies in mode="color" */
    "brightness": 100,  /* brightness, 0..100, applies in mode="white" */
    "white": 0,         /* white brightness, 0..255, applies in mode="color" */
    "temp": 4750,       /* color temperature in K, 3000..6500, applies in mode="white" */
    "effect": 0,        /* applies an effect when set */
    "turn": "on"        /* "on", "off" or "toggle" */
}

```

`mode` controls which set of parameters are used:

* `red`, `green`, `blue`, `white` and `gain` determine output power when `mode` is set to `color`
* `temp` and `brightness` determine output when `mode` is `white`

* `effect` is specified as an integer, see [description above](#shelly-bulb-device-modes)

A JSON payload will be published by Shelly Bulb on:

* `shellies/shellybulb-<deviceid>/color/0/status`

Subscribers can use this to obtain the latest device state.

```
{
    "ison": false,        /* whether the bulb is on */
    "has_timer": false,   /* whether a timer is currently armed */
    "timer_started": 0,   /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration": 0,  /* timer duration, s */
    "timer_remaining": 0, /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "mode": "color",      /* currently configured mode */
    "red": 255,           /* red brightness, 0..255, applies in mode="color" */
    "green": 125,         /* green brightness, 0..255, applies in mode="color" */
    "blue": 0,            /* blue brightness, 0..255, applies in mode="color" */
    "white": 0,           /* white brightness, 0..255, applies in mode="color" */
    "gain": 100,          /* gain for all channels, 0..100, applies in mode="color" */
    "temp": 5406,         /* color temperature in K, 3000..6500, applies in mode="white" */
    "brightness": 90,     /* brightness, 0..100, applies in mode="white" */
    "effect": 0           /* currently applied effect */
}

```

Shelly Bulb: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Bulb SHBLB-1 white-mode](docs/coiot/v2/examples/Shelly%20Bulb%20SHBLB-1%20white-mode)
* [Shelly Bulb SHBLB-1 color-mode](docs/coiot/v2/examples/Shelly%20Bulb%20SHBLB-1%20color-mode)

Shelly Bulb: `/settings`
----------

```

GET /settings

{
    "mode": "white",
    "actions": {
        "active": false,
        "names": [
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "ison": false,
            "red": 255,
            "green": 127,
            "blue": 0,
            "white": 0,
            "gain": 100,
            "temp": 5406,
            "brightness": 90,
            "effect": 0,
            "default_state": "last",
            "auto_on": 0,
            "auto_off": 0,
            "power": 0,
            "schedule": false,
            "schedule_rules": []
        }
    ]
}

```

The mode of operation of Shelly Bulb can be set here, along with [other standard settings](#settings).

### Attributes ###

|Attribute|     Type      |                                                                          Description                                                                          |
|---------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode`  |    string     |                                                                   Currently configured mode                                                                   |
|`actions`|     hash      |               List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-bulb-settings-actions)                |
|`lights` |array of hashes|Output channel settings. Shelly Bulb only supports a single channel, indexed as `0`. See [`/settings/light/0`](#shelly-bulb-settings-light-0) for more details.|

### Parameters ###

|Parameter| Type |                                 Description                                 |
|---------|------|-----------------------------------------------------------------------------|
| `mode`  |string|                   Accepted values are `white` and `color`                   |
|`actions`| hash |For setting actions, see [`/settings/actions`](#shelly-bulb-settings-actions)|

Shelly Bulb: `/settings/actions`
----------

```

GET /settings/actions
{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Bulb supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|   Action    |Index|              Description               |
|-------------|-----|----------------------------------------|
|out\_on\_url |  0  | URL to access when output is activated |
|out\_off\_url|  0  |URL to access when output is deactivated|

Shelly Bulb: `/settings/light/0`
----------

```

GET /settings/light/0

{
    "ison": false,
    "red": 255,
    "green": 127,
    "blue": 0,
    "white": 0,
    "gain": 100,
    "temp": 5406,
    "brightness": 90,
    "effect": 0,
    "default_state": "last",
    "auto_on": 0,
    "auto_off": 0,
    "power": 0,
    "schedule": false,
    "schedule_rules": []
}

```

### Attributes ###

|   Attribute    |      Type      |                                                    Description                                                     |
|----------------|----------------|--------------------------------------------------------------------------------------------------------------------|
|     `ison`     |      bool      |                                           Whether the bulb is on or off                                            |
|     `red`      |     number     |                                Red brightness, `0..255`, applies in `mode="color"`                                 |
|    `green`     |     number     |                               Green brightness, `0..255`, applies in `mode="color"`                                |
|     `blue`     |     number     |                                Blue brightness, `0..255`, applies in `mode="color"`                                |
|    `white`     |     number     |                               White brightness, `0..255`, applies in `mode="color"`                                |
|     `gain`     |     number     |                             Gain for all channels, `0..100`, applies in `mode="color"`                             |
|     `temp`     |     number     |                          Color temperature in K, `3000..6500`, applies in `mode="white"`                           |
|  `brightness`  |     number     |                                  Brightness, `0..100`, applies in `mode="white"`                                   |
|    `effect`    |     number     |                         Currently applied effect, [description](#shelly-bulb-device-modes)                         |
|`default_state` |     string     |                                            One of `on`, `off` or `last`                                            |
|   `auto_on`    |     number     |                                                ON-timer value, `s`                                                 |
|   `auto_off`   |     number     |                                                OFF-timer value, `s`                                                |
|    `power`     |     number     |User power constant to display in `meters` when bulb is on, see [`/settings/power/0`](#shelly-bulb-settings-power-0)|
|   `schedule`   |      bool      |                                           Whether scheduling is enabled                                            |
|`schedule_rules`|array of strings|                                           Rules for schedule activation                                            |

### Parameters ###

|   Parameter    |      Type      |                                Description                                |
|----------------|----------------|---------------------------------------------------------------------------|
|    `reset`     |      any       |      Any non-zero-length value will reset light settings to default       |
|    `effect`    |     number     |      Applies an effect, see [description](#shelly-bulb-device-modes)      |
|`default_state` |     string     |         Sets default power-on state, one of `on`, `off` or `last`         |
|   `auto_on`    |     number     |Sets a default timer to turn the bulb ON after every OFF command in seconds|
|   `auto_off`   |     number     |Sets a default timer to turn the bulb OFF after every ON command in seconds|
|   `schedule`   |      bool      |                           Enable schedule timer                           |
|`schedule_rules`|array of strings|           Rules for schedule activation, e.g. `0000-0123456-on`           |

Shelly Bulb: `/settings/color/0`
----------

Same as [`/settings/light/0`](#shelly-bulb-settings-light-0)

Shelly Bulb: `/settings/white/0`
----------

Same as [`/settings/light/0`](#shelly-bulb-settings-light-0)

Shelly Bulb: `/settings/power/0`
----------

### Parameters ###

|Parameter| Type |                             Description                              |
|---------|------|----------------------------------------------------------------------|
| `power` |number|User power constant to display in `meters` when bulb is on, `0..4000W`|

Shelly Bulb: `/status`
----------

```

GET /status

{
    "lights": [
        {
            "ison": false,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "color",
            "red": 255,
            "green": 127,
            "blue": 0,
            "white": 0,
            "gain": 100,
            "temp": 5406,
            "brightness": 90,
            "effect": 0
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true
        }
    ]
}

```

### Attributes ###

|Attribute|     Type      |                                                     Description                                                      |
|---------|---------------|----------------------------------------------------------------------------------------------------------------------|
|`lights` |array of hashes|Contains the current state of the light channels. See [`/light/0`](#shelly-bulb-light-0) for description of attributes|
|`meters` |array of hashes|                                       Power information, see description below                                       |

### `meters` attributes ###

|Attribute | Type |                                                              Description                                                               |
|----------|------|----------------------------------------------------------------------------------------------------------------------------------------|
| `power`  |number|When bulb is on, displays the value of the user power constant (see [`/settings/power/0`](#shelly-bulb-settings-power-0)); otherwise `0`|
|`is_valid`| bool |                                                             Always `true`                                                              |

Shelly Bulb: `/light/0`
----------

```

GET /light/0

{
    "ison": false,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "mode": "color",
    "red": 255,
    "green": 127,
    "blue": 0,
    "white": 0,
    "gain": 100,
    "temp": 5406,
    "brightness": 90,
    "effect": 0
}

```

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|     `mode`      |string|                                  Currently configured mode                                   |
|      `red`      |number|                     Red brightness, `0..255`, applies in `mode="color"`                      |
|     `green`     |number|                    Green brightness, `0..255`, applies in `mode="color"`                     |
|     `blue`      |number|                     Blue brightness, `0..255`, applies in `mode="color"`                     |
|     `white`     |number|                    White brightness, `0..255`, applies in `mode="color"`                     |
|     `gain`      |number|                  Gain for all channels, `0..100`, applies in `mode="color"`                  |
|     `temp`      |number|               Color temperature in K, `3000..6500`, applies in `mode="white"`                |
|  `brightness`   |number|                       Brightness, `0..100`, applies in `mode="white"`                        |
|    `effect`     |number|              Currently applied effect, [description](#shelly-bulb-device-modes)              |

### Parameters ###

This endpoint allows sending commands to the bulb to control it.

| Parameter  | Type |                             Description                             |
|------------|------|---------------------------------------------------------------------|
|   `mode`   |string|               Accepted values are `white` and `color`               |
|  `timer`   |number|Automatic flip-back timer in seconds, used in combination with `turn`|
|   `turn`   |string|               Command to turn `on`, `off` or `toggle`               |
|   `red`    |number|         Red brightness, `0..255`, applies in `mode="color"`         |
|  `green`   |number|        Green brightness, `0..255`, applies in `mode="color"`        |
|   `blue`   |number|        Blue brightness, `0..255`, applies in `mode="color"`         |
|  `white`   |number|        White brightness, `0..255`, applies in `mode="color"`        |
|   `gain`   |number|     Gain for all channels, `0..100`, applies in `mode="color"`      |
|   `temp`   |number|   Color temperature in K, `3000..6500`, applies in `mode="white"`   |
|`brightness`|number|           Brightness, `0..100`, applies in `mode="white"`           |
|  `effect`  |number|   Applies an effect, see [description](#shelly-bulb-device-modes)   |

Shelly Bulb: `/color/0`
----------

Same as [`/light/0`](#shelly-bulb-light-0)

Shelly Bulb: `/white/0`
----------

Same as [`/light/0`](#shelly-bulb-light-0)

Shelly Vintage
==========

Shelly Vintage: Overview
----------

**Shelly Vintage** - Wi-Fi on board, Cloud and MQTT enabled, dimmable, voice control, smart Wake-up and Night mode. Visit the product page for detailed information and User Manual:

<https://shelly.cloud/products/shelly-vintage-smart-home-automation-bulb/>

Shelly Vintage supports up to 20 schedule rules.

### Factory Reset ###

Factory reset can be performed by:

* powering the device ON and then OFF 5 times in a row in 5-second intervals
* via the web interface of the device

Performing factory reset will revert all settings to their initial values.

Shelly Vintage: MQTT
----------

To control the bulb with a simple on-off switch functionality, use:

* `shellies/ShellyVintage-<deviceid>/light/0/command` accepts `on` and `off` payloads
* `shellies/ShellyVintage-<deviceid>/light/0` is used by the device to report its current on-off state

For controlling other parameters of the light channel publish to:

* `shellies/ShellyVintage-<deviceid>/light/0/set`

The device expects a JSON payload on this topic, with the following sample contents:

```
{
    "brightness": 100,  /* brightness, 0..100 */
    "turn": "on",       /* "on", "off" or "toggle" */
    "transition": 500   /* One-shot transition, `0..5000` [ms] */
}

```

A JSON payload will be published by Shelly Vintage on:

* `shellies/ShellyVintage-<deviceid>/light/0/status`

Subscribers can use this to obtain the latest device state.

```
{
    "ison": false,        /* whether the bulb is on */
    "has_timer": false,   /* whether a timer is currently armed */
    "timer_started": 0,   /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration": 0,  /* timer duration, s */
    "timer_remaining": 0, /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "brightness": 90      /* brightness, 0..100 */
}

```

Power and energy info can be obtained at:

* `shellies/ShellyVintage-<deviceid>/light/0/power` reports instantaneous power consumption rate in Watts
* `shellies/ShellyVintage-<deviceid>/light/0/energy` reports amount of energy consumed in Watt-minute

Shelly Vintage: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Vintage SHVIN-1](docs/coiot/v2/examples/Shelly%20Vintage%20SHVIN-1)

Shelly Vintage: `/settings`
----------

```

GET /settings

{
    "mode": "white",
    "transition": 1000,
    "actions": {
        "active": false,
        "names": [
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "name": null,
            "ison": false,
            "brightness": 100,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "night_mode": {
                "enabled": false,
                "start_time": "00:00",
                "end_time": "00:00",
                "brightness": 0
            },
            "schedule_rules": []
        }
    ],
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 0
    }
}

```

The mode of operation of Shelly Vintage can be set here, along with [other standard settings](#settings).

### Attributes ###

| Attribute  |     Type      |                                                                             Description                                                                             |
|------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `mode`   |    string     |                                                    Currently configured mode, always `white` for Shelly Vintage                                                     |
|`transition`|    number     |                                                                    On/off transition time, `ms`                                                                     |
| `actions`  |     hash      |                 List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-vintage-settings-actions)                 |
|  `lights`  |array of hashes|Output channel settings. Shelly Vintage only supports a single channel, indexed as `0`. See [`/settings/light/0`](#shelly-vintage-settings-light-0) for more details.|
|`night_mode`|     hash      |                               Nightmode settings, see [`/settings/night_mode`](#shelly-vintage-settings-night_mode) for more details.                               |

### Parameters ###

| Parameter  | Type |                                  Description                                   |
|------------|------|--------------------------------------------------------------------------------|
|`transition`|number|                    Set on/off transition time, `0..5000ms`                     |
| `actions`  | hash |For setting actions, see [`/settings/actions`](#shelly-vintage-settings-actions)|

Shelly Vintage: `/settings/actions`
----------

```

GET /settings/actions
{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Vintage supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|   Action    |Index|              Description               |
|-------------|-----|----------------------------------------|
|out\_on\_url |  0  | URL to access when output is activated |
|out\_off\_url|  0  |URL to access when output is deactivated|

Shelly Vintage: `/settings/light/0`
----------

```

GET /settings/light/0

{
    "name": null,
    "ison": false,
    "brightness": 100,
    "default_state": "on",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 0
    },
    "schedule_rules": []
}

```

### Attributes ###

|   Attribute    |      Type      |                                              Description                                              |
|----------------|----------------|-------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                             Channel name                                              |
|     `ison`     |      bool      |                                     Whether the bulb is on or off                                     |
|  `brightness`  |     number     |                                         Brightness, `0..100`                                          |
|`default_state` |     string     |                                     One of `on`, `off` or `last`                                      |
|   `auto_on`    |     number     |                                          ON-timer value, `s`                                          |
|   `auto_off`   |     number     |                                         OFF-timer value, `s`                                          |
|   `schedule`   |      bool      |                                     Whether scheduling is enabled                                     |
|  `night_mode`  |      hash      |Nightmode settings, see [`/settings/night_mode`](#shelly-vintage-settings-night_mode) for more details.|
|`schedule_rules`|array of strings|                                     Rules for schedule activation                                     |

### Parameters ###

|   Parameter    |      Type      |                                Description                                |
|----------------|----------------|---------------------------------------------------------------------------|
|     `name`     |     string     |                             Set channel name                              |
|    `reset`     |      any       |      Any non-zero-length value will reset light settings to default       |
|`default_state` |     string     |         Sets default power-on state, one of `on`, `off` or `last`         |
|   `auto_on`    |     number     |Sets a default timer to turn the bulb ON after every OFF command in seconds|
|   `auto_off`   |     number     |Sets a default timer to turn the bulb OFF after every ON command in seconds|
|   `schedule`   |      bool      |                           Enable schedule timer                           |
|`schedule_rules`|array of strings|           Rules for schedule activation, e.g. `0000-0123456-on`           |

Shelly Vintage: `/settings/night_mode`
----------

```

GET /settings/night_mode

{
    "enabled": false,
    "start_time": "00:00",
    "end_time": "00:00",
    "brightness": 0
}

```

### Parameters ###

| Parameter  | Type |                Description                |
|------------|------|-------------------------------------------|
| `enabled`  | bool |         Enable/disable night mode         |
|`start_time`|string|Set night mode start time in format `hh:mm`|
| `end_time` |string| Set night mode end time in format `hh:mm` |
|`brightness`|number|Set brightness when in night mode, `0..100`|

Shelly Vintage: `/status`
----------

```

GET /status

{
    "lights": [
        {
            "ison": false,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "brightness": 90,
            "transition": 500
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ]
}

```

### Attributes ###

|Attribute|     Type      |                                                      Description                                                       |
|---------|---------------|------------------------------------------------------------------------------------------------------------------------|
|`lights` |array of hashes|Contains the current state of the light channel. See [`/light/0`](#shelly-vintage-light-0) for description of attributes|
|`meters` |array of hashes|                                        Power information, see description below                                        |

### `meters` attributes ###

### Attributes ###

| Attribute |      Type      |                             Description                             |
|-----------|----------------|---------------------------------------------------------------------|
|  `power`  |     number     |             Current real AC power being drawn, in Watts             |
|`is_valid` |      bool      |                Whether power metering self-checks OK                |
|`timestamp`|     number     |Timestamp of the last energy counter value, with the applied timezone|
|`counters` |array of numbers|  Energy counter value for the last 3 round minutes in Watt-minute   |
|  `total`  |     number     |                Total energy consumed in Watt-minute                 |

Shelly Vintage: `/light/0`
----------

```

GET /light/0

{
    "ison": false,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "brightness": 90,
    "transition": 500
}

```

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|  `brightness`   |number|                                     Brightness, `0..100`                                     |
|  `transition`   |number|                             One-shot transition, `0..5000` [ms]                              |

### Parameters ###

This endpoint allows sending commands to the bulb to control it.

| Parameter  | Type |                             Description                             |
|------------|------|---------------------------------------------------------------------|
|   `turn`   |string|               Command to turn `on`, `off` or `toggle`               |
|  `timer`   |number|Automatic flip-back timer in seconds, used in combination with `turn`|
|`brightness`|number|                      Set brightness, `0..100`                       |
|`transition`|number|                 One-shot transition, `0..5000` [ms]                 |

Shelly Duo
==========

Shelly Duo: Overview
----------

**Shelly Duo** - Wi-Fi on board, Cloud and MQTT enabled, dimmable, 2700K up to 6500K, voice control, smart Wake-up and Night mode. Visit the product page for detailed information and User Manual:

<https://shelly.cloud/products/shelly-duo-smart-home-automation-bulb/>

Shelly Duo supports up to 20 schedule rules.

### Factory Reset ###

Factory reset can be performed by:

* powering the device ON and then OFF 5 times in a row in 5-second intervals
* via the web interface of the device

Performing factory reset will revert all settings to their initial values.

Shelly Duo: MQTT
----------

To control the bulb with a simple on-off switch functionality, use:

* `shellies/ShellyBulbDuo-<deviceid>/light/0/command` accepts `on` and `off` payloads
* `shellies/ShellyBulbDuo-<deviceid>/light/0` is used by the device to report its current on-off state

For controlling other parameters of the light channel publish to:

* `shellies/ShellyBulbDuo-<deviceid>/light/0/set`

The device expects a JSON payload on this topic, with the following sample contents:

```
{
    "brightness": 100,  /* brightness, 0..100 */
    "white": 0,         /* white level, 0..100 */
    "temp": 2700,       /* color temperature in K, 2700..6500 */
    "turn": "on",       /* "on", "off" or "toggle" */
    "transition": 500   /* One-shot transition, `0..5000` [ms] */
}

```

A JSON payload will be published by Shelly Duo on:

* `shellies/ShellyBulbDuo-<deviceid>/light/0/status`

Subscribers can use this to obtain the latest device state.

```
{
    "ison": false,        /* whether the channel is turned ON or OFF */
    "has_timer": false,   /* whether a timer is currently armed for this channel */
    "timer_started": 0,   /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration": 0,  /* timer duration, s */
    "timer_remaining": 0, /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "brightness": 100,    /* brightness, 0..100 */
    "white": 0,           /* white level, 0..100 */
    "temp": 2700          /* color temperature, 2700..6500K */
}

```

Power and energy info can be obtained at:

* `shellies/ShellyBulbDuo-<deviceid>/light/0/power` reports instantaneous power consumption rate in Watts
* `shellies/ShellyBulbDuo-<deviceid>/light/0/energy` reports amount of energy consumed in Watt-minute

Shelly Duo: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Duo SHBDUO-1](docs/coiot/v2/examples/Shelly%20Duo%20SHBDUO-1)

Shelly Duo: `/settings`
----------

```

GET /settings

{
    "device": {
      "submodel": 2
    },
    "mode": "white",
    "transition": 1000,
    "actions": {
        "active": false,
        "names": [
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "name": null,
            "ison": false,
            "brightness": 100,
            "white": 50,
            "temp": 4600,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "night_mode": {
                "enabled": false,
                "start_time": "00:00",
                "end_time": "00:00",
                "brightness": 0
            },
            "schedule_rules": []
        }
    ],
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 0
    }
}

```

The mode of operation of Shelly Duo can be set here, along with [other standard settings](#settings).

### Attributes ###

|    Attribute    |     Type      |                                                                         Description                                                                         |
|-----------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`device_submodel`|    number     |                                      Currently configured device submodel: `0` for Unknown, `1` for E27, `2` for GU10                                       |
|     `mode`      |    string     |                                                  Currently configured mode, always `white` for Shelly Duo                                                   |
|  `transition`   |    number     |                                                                On/off transition time, `ms`                                                                 |
|    `actions`    |     hash      |             List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-vintage-settings-actions)             |
|    `lights`     |array of hashes|Output channel settings. Shelly Duo only supports a single channel, indexed as `0`. See [`/settings/light/0`](#shelly-duo-settings-light-0) for more details.|
|  `night_mode`   |     hash      |                             Nightmode settings, see [`/settings/night_mode`](#shelly-duo-settings-night_mode) for more details.                             |

### Parameters ###

|    Parameter    | Type |                                  Description                                   |
|-----------------|------|--------------------------------------------------------------------------------|
|`device_submodel`|number|Currently configured device submodel: `0` for Unknown, `1` for E27, `2` for GU10|
|  `transition`   |number|                    Set on/off transition time, `0..5000ms`                     |
|    `actions`    | hash |For setting actions, see [`/settings/actions`](#shelly-vintage-settings-actions)|

Shelly Duo: `/settings/actions`
----------

```

GET /settings/actions
{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Duo supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|   Action    |Index|              Description               |
|-------------|-----|----------------------------------------|
|out\_on\_url |  0  | URL to access when output is activated |
|out\_off\_url|  0  |URL to access when output is deactivated|

Shelly Duo: `/settings/light/0`
----------

```

GET /settings/light/0

{
    "name": null,
    "ison": false,
    "brightness": 100,
    "white": 50,
    "temp": 4600,
    "default_state": "on",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 0
    },
    "schedule_rules": []
}

```

### Attributes ###

|   Attribute    |      Type      |                                            Description                                            |
|----------------|----------------|---------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                           Channel name                                            |
|     `ison`     |      bool      |                                   Whether the bulb is on or off                                   |
|  `brightness`  |     number     |                                       Brightness, `0..100`                                        |
|    `white`     |     number     |                                       White level, `0..100`                                       |
|     `temp`     |     number     |                      Color temperature, `2700..6500K` (derived from `white`)                      |
|`default_state` |     string     |                                   One of `on`, `off` or `last`                                    |
|   `auto_on`    |     number     |                                        ON-timer value, `s`                                        |
|   `auto_off`   |     number     |                                       OFF-timer value, `s`                                        |
|   `schedule`   |      bool      |                                   Whether scheduling is enabled                                   |
|  `night_mode`  |      hash      |Nightmode settings, see [`/settings/night_mode`](#shelly-duo-settings-night_mode) for more details.|
|`schedule_rules`|array of strings|                                   Rules for schedule activation                                   |

### Parameters ###

|   Parameter    |      Type      |                                Description                                |
|----------------|----------------|---------------------------------------------------------------------------|
|     `name`     |     string     |                             Set channel name                              |
|    `reset`     |      any       |      Any non-zero-length value will reset light settings to default       |
|`default_state` |     string     |         Sets default power-on state, one of `on`, `off` or `last`         |
|   `auto_on`    |     number     |Sets a default timer to turn the bulb ON after every OFF command in seconds|
|   `auto_off`   |     number     |Sets a default timer to turn the bulb OFF after every ON command in seconds|
|   `schedule`   |      bool      |                           Enable schedule timer                           |
|`schedule_rules`|array of strings|           Rules for schedule activation, e.g. `0000-0123456-on`           |

Shelly Duo: `/settings/night_mode`
----------

```

GET /settings/night_mode

{
    "enabled": false,
    "start_time": "00:00",
    "end_time": "00:00",
    "brightness": 0
}

```

### Parameters ###

| Parameter  | Type |                Description                |
|------------|------|-------------------------------------------|
| `enabled`  | bool |         Enable/disable night mode         |
|`start_time`|string|Set night mode start time in format `hh:mm`|
| `end_time` |string| Set night mode end time in format `hh:mm` |
|`brightness`|number|Set brightness when in night mode, `0..100`|

Shelly Duo: `/status`
----------

```

GET /status

{
    "lights": [
        {
            "ison": false,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "brightness": 90,
            "white": 0,
            "temp": 2700,
            "transition": 500
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ]
}

```

### Attributes ###

|Attribute|     Type      |                                                     Description                                                     |
|---------|---------------|---------------------------------------------------------------------------------------------------------------------|
|`lights` |array of hashes|Contains the current state of the light channels. See [`/light/0`](#shelly-duo-light-0) for description of attributes|
|`meters` |array of hashes|                                      Power information, see description below                                       |

### `meters` attributes ###

| Attribute |      Type      |                             Description                             |
|-----------|----------------|---------------------------------------------------------------------|
|  `power`  |     number     |                         Consumed power, `W`                         |
|`is_valid` |      bool      |                            Always `true`                            |
|`timestamp`|     number     |Timestamp of the last energy counter value, with the applied timezone|
|`counters` |array of numbers|  Energy counter value for the last 3 round minutes in Watt-minute   |
|  `total`  |     number     |                Total energy consumed in Watt-minute                 |

Shelly Duo: `/light/0`
----------

```

GET /light/0

{
    "ison": false,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "brightness": 90,
    "white": 0,
    "temp": 2700,
    "transition": 500
}

```

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|  `brightness`   |number|                                     Brightness, `0..100`                                     |
|     `white`     |number|                                    White level, `0..100`                                     |
|     `temp`      |number|                   Color temperature, `2700..6500K` (derived from `white`)                    |
|  `transition`   |number|                             One-shot transition, `0..5000` [ms]                              |

### Parameters ###

This endpoint allows sending commands to the bulb to control it.

| Parameter  | Type |                             Description                             |
|------------|------|---------------------------------------------------------------------|
|   `turn`   |string|               Command to turn `on`, `off` or `toggle`               |
|  `timer`   |number|Automatic flip-back timer in seconds, used in combination with `turn`|
|`brightness`|number|                        Brightness, `0..100`                         |
|  `white`   |number|                        White level, `0..100`                        |
|   `temp`   |number|                Color temperature in K, `2700..6500`                 |
|`transition`|number|                 One-shot transition, `0..5000` [ms]                 |

Shelly Bulb RGBW
==========

Shelly Bulb RGBW: Overview
----------

**Shelly Bulb RGBW** is a WiFi-enabled E27 bulb with Red, Green, Blue and White LEDs. Visit the product page for detailed information and User Manual:

<https://shelly.cloud/products/shelly-bulb-smart-home-automation-device/>

A number of exposed endpoints allow configuring all aspects of Shelly Bulb RGBW:

* controlling device configuration including WiFi mode and device mode and device-specific options
* controlling brightness and color of the bulb

Shelly Bulb RGBW supports up to 20 schedule rules.

### Factory Reset ###

Factory reset can be performed by:

* powering the device ON and then OFF 5 times in a row in 5-second intervals
* via the web interface of the device

Performing factory reset will revert all settings to their initial values.

Shelly Bulb RGBW: Device Modes
----------

Shelly Color can operate in two distinct device modes:

* **Color**
* **Warm/Cold White**

In **Color** mode, each output channel: Red, Green, Blue and White is individually controllable.

In **Warm/Cold White** mode the device accepts color temperature and brightness and adjusts power output to produce the desired white light.

Shelly Bulb RGBW can also play a set of pre-defined effects, specified by a numerical index:

* `0` - Off
* `1` - Meteor Shower
* `2` - Gradual Change
* `3` - Flash

Shelly Bulb RGBW: MQTT
----------

Shelly Bulb RGBW allows the simple `on` and `off` commands, as well as setting the color, brightness and effects using a JSON payload.

To control the bulb with a simple on-off switch functionality, use:

* `shellies/shellycolorbulb-<deviceid>/color/0/command` accepts `on` and `off` payloads
* `shellies/shellycolorbulb-<deviceid>/color/0` is used by the device to report its current on-off state

For controlling other parameters of the LED channels publish to:

* `shellies/shellycolorbulb-<deviceid>/color/0/set`

The device expects a JSON payload on this topic, with the following sample contents:

```
{
    "mode": "color",    /* "color" or "white" */
    "red": 0,           /* red brightness, 0..255, applies in mode="color" */
    "green": 0,         /* green brightness, 0..255, applies in mode="color" */
    "blue": 255,        /* blue brightness, 0..255, applies in mode="color" */
    "gain": 100,        /* gain for all channels, 0..100, applies in mode="color" */
    "brightness": 100,  /* brightness, 0..100, applies in mode="white" */
    "white": 0,         /* white brightness, 0..255, applies in mode="color" */
    "temp": 4750,       /* color temperature in K, 3000..6500, applies in mode="white" */
    "effect": 0,        /* applies an effect when set */
    "turn": "on",       /* "on", "off" or "toggle" */
  "transition": 500   /* One-shot transition, `0..5000` [ms] */
}

```

`mode` controls which set of parameters are used:

* `red`, `green`, `blue`, `white` and `gain` determine output power when `mode` is set to `color`
* `temp` and `brightness` determine output when `mode` is `white`

* `effect` is specified as an integer, see [description above](#shelly-bulb-rgbw-device-modes)

A JSON payload will be published by Shelly Bulb RGBW on:

* `shellies/shellycolorbulb-<deviceid>/color/0/status`

Subscribers can use this to obtain the latest device state.

```
{
    "ison": false,        /* whether the bulb is on */
    "has_timer": false,   /* whether a timer is currently armed */
    "timer_started": 0,   /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration": 0,  /* timer duration, s */
    "timer_remaining": 0, /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "mode": "color",      /* currently configured mode */
    "red": 255,           /* red brightness, 0..255, applies in mode="color" */
    "green": 125,         /* green brightness, 0..255, applies in mode="color" */
    "blue": 0,            /* blue brightness, 0..255, applies in mode="color" */
    "white": 0,           /* white brightness, 0..255, applies in mode="color" */
    "gain": 100,          /* gain for all channels, 0..100, applies in mode="color" */
    "temp": 5406,         /* color temperature in K, 3000..6500, applies in mode="white" */
    "brightness": 90,     /* brightness, 0..100, applies in mode="white" */
    "effect": 0           /* currently applied effect */
}

```

Power and energy info can be obtained at:

* `shellies/shellycolorbulb-<deviceid>/light/0/power` reports instantaneous power consumption rate in Watts
* `shellies/shellycolorbulb-<deviceid>/light/0/energy` reports amount of energy consumed in Watt-minute

Shelly Bulb RGBW: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Bulb RGBW SHCB-1 white-mode](docs/coiot/v2/examples/Shelly%20Bulb%20RGBW%20SHCB-1%20white-mode)
* [Shelly Bulb RGBW SHCB-1 color-mode](docs/coiot/v2/examples/Shelly%20Bulb%20RGBW%20SHCB-1%20color-mode)

Shelly Bulb RGBW: `/settings`
----------

```

GET /settings

{
    "device": {
      "submodel": 2
    },
    "mode": "white",
    "actions": {
        "active": false,
        "names": [
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "ison": false,
            "red": 255,
            "green": 127,
            "blue": 0,
            "white": 0,
            "gain": 100,
            "temp": 5406,
            "brightness": 90,
            "transition": 1000,
            "effect": 0,
            "default_state": "last",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "night_mode": {
                "enabled": false,
                "start_time": "00:00",
                "end_time": "00:00",
                "brightness": 0
            },
            "schedule_rules": []
        }
    ],
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 0
    }
}

```

The mode of operation of Shelly Bulb RGBW can be set here, along with [other standard settings](#settings).

### Attributes ###

|    Attribute    |     Type      |                                                                               Description                                                                               |
|-----------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `mode`      |    string     |                                                                        Currently configured mode                                                                        |
|`device_submodel`|    number     |                                            Currently configured device submodel: `0` for Unknown, `1` for E27, `2` for GU10                                             |
|    `actions`    |     hash      |                  List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-bulb-rgbw-settings-actions)                  |
|    `lights`     |array of hashes|Output channel settings. Shelly Bulb RGBW only supports a single channel, indexed as `0`. See [`/settings/light/0`](#shelly-bulb-rgbw-settings-light-0) for more details.|
|  `night_mode`   |     hash      |                                Nightmode settings, see [`/settings/night_mode`](#shelly-bulb-rgbw-settings-night_mode) for more details.                                |

### Parameters ###

|    Parameter    | Type |                                   Description                                    |
|-----------------|------|----------------------------------------------------------------------------------|
|     `mode`      |string|                     Accepted values are `white` and `color`                      |
|`device_submodel`|number|         Set device submodel: `0` for Unknown, `1` for E27, `2` for GU10          |
|    `actions`    | hash |For setting actions, see [`/settings/actions`](#shelly-bulb-rgbw-settings-actions)|

Shelly Bulb RGBW: `/settings/actions`
----------

```

GET /settings/actions
{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Bulb RGBW supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|   Action    |Index|              Description               |
|-------------|-----|----------------------------------------|
|out\_on\_url |  0  | URL to access when output is activated |
|out\_off\_url|  0  |URL to access when output is deactivated|

Shelly Bulb RGBW: `/settings/light/0`
----------

```

GET /settings/light/0

{
    "ison": false,
    "red": 255,
    "green": 127,
    "blue": 0,
    "white": 0,
    "gain": 100,
    "temp": 5406,
    "brightness": 90,
    "transition": 1000,
    "effect": 0,
    "default_state": "last",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 0
    },
    "schedule_rules": []
}

```

### Attributes ###

|   Attribute    |      Type      |                                               Description                                               |
|----------------|----------------|---------------------------------------------------------------------------------------------------------|
|     `ison`     |      bool      |                                      Whether the bulb is on or off                                      |
|     `red`      |     number     |                           Red brightness, `0..255`, applies in `mode="color"`                           |
|    `green`     |     number     |                          Green brightness, `0..255`, applies in `mode="color"`                          |
|     `blue`     |     number     |                          Blue brightness, `0..255`, applies in `mode="color"`                           |
|    `white`     |     number     |                          White brightness, `0..255`, applies in `mode="color"`                          |
|     `gain`     |     number     |                       Gain for all channels, `0..100`, applies in `mode="color"`                        |
|     `temp`     |     number     |                     Color temperature in K, `3000..6500`, applies in `mode="white"`                     |
|  `brightness`  |     number     |                             Brightness, `0..100`, applies in `mode="white"`                             |
|  `transition`  |     number     |                                   On/Off transiiton time, [0-5000] ms                                   |
|    `effect`    |     number     |                 Currently applied effect, [description](#shelly-bulb-rgbw-device-modes)                 |
|`default_state` |     string     |                                      One of `on`, `off` or `last`                                       |
|   `auto_on`    |     number     |                                           ON-timer value, `s`                                           |
|   `auto_off`   |     number     |                                          OFF-timer value, `s`                                           |
|   `schedule`   |      bool      |                                      Whether scheduling is enabled                                      |
|  `night_mode`  |      hash      |Nightmode settings, see [`/settings/night_mode`](#shelly-bulb-rgbw-settings-night_mode) for more details.|
|`schedule_rules`|array of strings|                                      Rules for schedule activation                                      |

### Parameters ###

|   Parameter    |      Type      |                                Description                                |
|----------------|----------------|---------------------------------------------------------------------------|
|    `reset`     |      any       |      Any non-zero-length value will reset light settings to default       |
|    `effect`    |     number     |   Applies an effect, see [description](#shelly-bulb-rgbw-device-modes)    |
|  `transition`  |     number     |                 Sets On/Off transiiton time, [0-5000] ms                  |
|`default_state` |     string     |         Sets default power-on state, one of `on`, `off` or `last`         |
|   `auto_on`    |     number     |Sets a default timer to turn the bulb ON after every OFF command in seconds|
|   `auto_off`   |     number     |Sets a default timer to turn the bulb OFF after every ON command in seconds|
|   `schedule`   |      bool      |                           Enable schedule timer                           |
|`schedule_rules`|array of strings|           Rules for schedule activation, e.g. `0000-0123456-on`           |

Shelly Bulb RGBW: `/settings/color/0`
----------

Same as [`/settings/light/0`](#shelly-bulb-rgbw-settings-light-0)

Shelly Bulb RGBW: `/settings/white/0`
----------

Same as [`/settings/light/0`](#shelly-bulb-rgbw-settings-light-0)

Shelly Bulb RGBW: `/status`
----------

```

GET /status

{
    "lights": [
        {
            "ison": false,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "color",
            "red": 255,
            "green": 127,
            "blue": 0,
            "white": 0,
            "gain": 100,
            "temp": 5406,
            "brightness": 90,
            "effect": 0,
            "transition": 500
        }
    ],
    "meters": [
        {
            "power": 0,
            "is_valid": true,
            "timestamp": 0,
            "counters": [
              0.115,
              0.115,
              0.115
            ],
            "total": 4
        }
    ]
}

```

### Attributes ###

|Attribute|     Type      |                                                        Description                                                        |
|---------|---------------|---------------------------------------------------------------------------------------------------------------------------|
|`lights` |array of hashes|Contains the current state of the light channels. See [`/light/0`](#shelly-bulb-rgbw-light-0) for description of attributes|
|`meters` |array of hashes|                                         Power information, see description below                                          |

### `meters` attributes ###

| Attribute |      Type      |                             Description                             |
|-----------|----------------|---------------------------------------------------------------------|
|  `power`  |     number     |                         Consumed power, `W`                         |
|`is_valid` |      bool      |                            Always `true`                            |
|`timestamp`|     number     |Timestamp of the last energy counter value, with the applied timezone|
|`counters` |array of numbers|  Energy counter value for the last 3 round minutes in Watt-minute   |
|  `total`  |     number     |                Total energy consumed in Watt-minute                 |

Shelly Bulb RGBW: `/light/0`
----------

```

GET /light/0

{
    "ison": false,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "mode": "color",
    "red": 255,
    "green": 127,
    "blue": 0,
    "white": 0,
    "gain": 100,
    "temp": 5406,
    "brightness": 90,
    "effect": 0,
    "transition": 500
}

```

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|     `mode`      |string|                                  Currently configured mode                                   |
|      `red`      |number|                     Red brightness, `0..255`, applies in `mode="color"`                      |
|     `green`     |number|                    Green brightness, `0..255`, applies in `mode="color"`                     |
|     `blue`      |number|                     Blue brightness, `0..255`, applies in `mode="color"`                     |
|     `white`     |number|                    White brightness, `0..255`, applies in `mode="color"`                     |
|     `gain`      |number|                  Gain for all channels, `0..100`, applies in `mode="color"`                  |
|     `temp`      |number|               Color temperature in K, `3000..6500`, applies in `mode="white"`                |
|  `brightness`   |number|                       Brightness, `0..100`, applies in `mode="white"`                        |
|    `effect`     |number|           Currently applied effect, [description](#shelly-bulb-rgbw-device-modes)            |
|  `transition`   |number|                             One-shot transition, `0..5000` [ms]                              |

### Parameters ###

This endpoint allows sending commands to the bulb to control it.

| Parameter  | Type |                             Description                             |
|------------|------|---------------------------------------------------------------------|
|   `mode`   |string|               Accepted values are `white` and `color`               |
|  `timer`   |number|Automatic flip-back timer in seconds, used in combination with `turn`|
|   `turn`   |string|               Command to turn `on`, `off` or `toggle`               |
|   `red`    |number|         Red brightness, `0..255`, applies in `mode="color"`         |
|  `green`   |number|        Green brightness, `0..255`, applies in `mode="color"`        |
|   `blue`   |number|        Blue brightness, `0..255`, applies in `mode="color"`         |
|  `white`   |number|        White brightness, `0..255`, applies in `mode="color"`        |
|   `gain`   |number|     Gain for all channels, `0..100`, applies in `mode="color"`      |
|   `temp`   |number|   Color temperature in K, `3000..6500`, applies in `mode="white"`   |
|`brightness`|number|           Brightness, `0..100`, applies in `mode="white"`           |
|  `effect`  |number|Applies an effect, see [description](#shelly-bulb-rgbw-device-modes) |
|`transition`|number|                 One-shot transition, `0..5000` [ms]                 |

Shelly Bulb RGBW: `/color/0`
----------

Same as [`/light/0`](#shelly-bulb-rgbw-light-0)

Shelly Bulb RGBW: `/white/0`
----------

Same as [`/light/0`](#shelly-bulb-rgbw-light-0)

Shelly RGBW2 Color
==========

Shelly RGBW2 Color: Overview
----------

Shelly RGBW2 Color is a WiFi-enabled 4-channel 12V/24V LED driver which can control a single RGB+W installation. Via firmware change the same device can be used to control the 4 output channels independently, see [Shelly RGBW2 White](#shelly-rgbw2-white).

Shelly RGBW2 Color supports up to 7 schedule rules.

<https://shelly.cloud/products/shelly-rgbw2-smart-home-automation-led-controller/>

### Factory Reset ###

A factory reset can be performed over the local web interface or Shelly application. In case the device cannot be accessed over network, physical methods for factory reset exist:

* Using the external switch input: turn the device on/off 5 or more times within the first minute after power-on using the switch input terminal. This will trigger a complete factory reset.
* Using the built-in user button:
  * hold for 5 seconds to reset WiFi settings. The device will revert to AP mode.
  * hold for 10 seconds to perform a complete factory reset.

Shelly RGBW2 Color: MQTT
----------

The device can be controlled using the same MQTT protocol as [Shelly Bulb](#shelly-bulb-mqtt) and looks like a single logical device.

### Command topics ###

Shelly RGBW2 Color subscribes to the following topics:

* `shellies/shellyrgbw2-<deviceid>/color/0/command` accepts `on` and `off` payloads
* `shellies/shellyrgbw2-<deviceid>/color/0/set` accepts a JSON payload described below:

```
{
    "mode": "color",    /* "color" */
    "red": 0,           /* red brightness, 0..255 */
    "green": 0,         /* green brightness, 0..255 */
    "blue": 255,        /* blue brightness, 0..255 */
    "gain": 100,        /* gain for all channels, 0..100 */
    "white": 0,         /* white brightness, 0..255 */
    "effect": 0,        /* applies an effect when set */
    "turn": "on",       /* "on", "off" or "toggle" */
  "transition": 500   /* One-shot transition, `0..5000` [ms] */
}

```

### Status topics ###

Shelly RGBW2 Color publishes to:

* `shellies/shellyrgbw2-<deviceid>/input/0` reports the current state as `0` or `1`
* `shellies/shellyrgbw2-<deviceid>/longpush/0` reports a value indicating longpush state as `0` (shortpush) or `1` (longpush)
* `shellies/shellyrgbw2-<deviceid>/input_event/0` reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly-rgbw2-color-status) for details
* `shellies/shellyrgbw2-<deviceid>/color/0` current on/off state
* `shellies/shellyrgbw2-<deviceid>/color/0/status` a JSON payload described below:

```
{
    "ison",            /* whether the output is ON or OFF */
    "has_timer",       /* whether a timer is currently armed for this channel */
    "timer_started",   /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration",  /* timer duration, s */
    "timer_remaining", /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "mode",            /* currently configured mode */
    "red",             /* red brightness, 0..255 */
    "green",           /* green brightness, 0..255 */
    "blue",            /* blue brightness, 0..255 */
    "white",           /* white brightness, 0..255 */
    "gain",            /* gain for all channels, 0..100 */
    "effect",          /* applied effect */
    "power",           /* consumed power, W */
    "overpower"        /* whether an overpower condition has occurred */
}

```

Shelly RGBW2 Color: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly RGBW2-color SHRGBW2-color](docs/coiot/v2/examples/Shelly%20RGBW2-color%20SHRGBW2-color)

Shelly RGBW2 Color: `/settings`
----------

```

GET /settings

{
    "factory_reset_from_switch": true,
    "mode": "color",
    "alt_modes": ["white"],
    "dcpower": 1,
    "led_status_disable": false,
    "coiot": {
      "execute_enable": false
    },
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "btn_off_url",
            "btn_longpush_url",
            "btn_shortpush_url",
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "name": null,
            "ison": true,
            "red": 0,
            "green": 0,
            "blue": 255,
            "white": 0,
            "gain": 50,
            "effect": 0,
            "transition": 1000,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "night_mode": {
                "enabled": false,
                "start_time": "00:00",
                "end_time": "00:00",
                "brightness": 20
            },
            "btn_type": "toggle",
            "btn_reverse": 0,
            "schedule_rules": []
        }
    ],
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 20
    }
}

```

### Attributes ###

|         Attribute         |      Type      |                                                              Description                                                              |
|---------------------------|----------------|---------------------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|      bool      |                                 Whether factory reset via 5-time flip of the input switch is enabled                                  |
|          `mode`           |     string     |                                             Currently configured mode, `color` or `white`                                             |
|        `alt_modes`        |array of strings|                                                       Alternative device modes                                                        |
|         `dcpower`         |     number     |                                                  DC supply voltage `0`=12V, `1`=24V                                                   |
|   `led_status_disable`    |      bool      |                                               Whether LED status indication is enabled                                                |
|  `coiot.execute_enable`   |      bool      |                                      Whether the execution of light control commands is enabled                                       |
|         `actions`         |      hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-rgbw2-color-settings-actions)|
|         `lights`          |array of hashes |              Output channel settings. See [`/settings/color/0`](#shelly-rgbw2-color-settings-color-0) for more details.               |
|       `night_mode`        |      hash      |                      Night mode settings, see [`/settings/night_mode`](#shelly-rgbw2-color-settings-night_mode)                       |

### Parameters ###

|         Parameter         | Type |                                    Description                                     |
|---------------------------|------|------------------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |          Enable/disable factory reset via 5-time flip of the input switch          |
|          `mode`           |string|              Set to `color` or `white`; determines the operating mode              |
|   `led_status_disable`    | bool |                           Disable LED status indication                            |
|         `dcpower`         | bool |               Set to `true` for 24 V power supply, `false` for 12 V                |
|  `coiot_execute_enable`   | bool |                     Enable listening for color change commands                     |
|         `actions`         | hash |For setting actions, see [`/settings/actions`](#shelly-rgbw2-color-settings-actions)|

Shelly RGBW2 Color: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly RGBW2 Color supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action       |Index|                    Description                    |
|-------------------|-----|---------------------------------------------------|
|   `btn_on_url`    |  0  |   URL to access when input switch is activated    |
|   `btn_off_url`   |  0  |  URL to access when input switch is deactivated   |
|`btn_longpush_url` |  0  |   URL to access when input switch is held down.   |
|`btn_shortpush_url`|  0  |URL to access when input switch is pressed briefly.|
|   `out_on_url`    |  0  |      URL to access when output is activated       |
|   `out_off_url`   |  0  |     URL to access when output is deactivated      |

Shelly RGBW2 Color: `/settings/color/0`
----------

```

GET /settings/color/0

{
    "name": null,
    "ison": true,
    "red": 0,
    "green": 0,
    "blue": 255,
    "white": 0,
    "gain": 50,
    "effect": 0,
    "transition": 1000,
    "default_state": "on",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 20
    },
    "btn_type": "toggle",
    "btn_reverse": 0,
    "schedule_rules": []
}

```

### Attributes ###

|   Attribute    |      Type      |                                       Description                                        |
|----------------|----------------|------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                       Channel name                                       |
|     `ison`     |      bool      |                            Whether the outputs are ON or OFF                             |
|     `red`      |     number     |                                 Red brightness, `0..255`                                 |
|    `green`     |     number     |                                Green brightness, `0..255`                                |
|     `blue`     |     number     |                                Blue brightness, `0..255`                                 |
|    `white`     |     number     |                                White brightness, `0..255`                                |
|     `gain`     |     number     |                             Gain for all channels, `0..100`                              |
|    `effect`    |     number     |                          Applied effect, see description below                           |
|  `transition`  |     number     |               Transition time between on/off and color change, [0-5000] ms               |
|`default_state` |     string     |                               One of `on`, `off` or `last`                               |
|   `auto_on`    |     number     |                                   ON-timer value, `s`                                    |
|   `auto_off`   |     number     |                                   OFF-timer value, `s`                                   |
|   `btn_type`   |     string     |         Input type, one of `momentary`, `toggle`, `edge`, `detached` or `action`         |
| `btn_reverse`  |     number     |                    Whether the logical state of the input is inverted                    |
|   `schedule`   |      bool      |                              Whether scheduling is enabled                               |
|  `night_mode`  |      hash      |Night mode settings, see [`/settings/night_mode`](#shelly-rgbw2-color-settings-night_mode)|
|`schedule_rules`|array of strings|                  Rules for schedule activation, e.g. `0000-0123456-on`                   |

This endpoint sets persistent settings for `color` mode:

### Parameters ###

|   Parameter    |      Type      |                           Description                            |
|----------------|----------------|------------------------------------------------------------------|
|     `name`     |     string     |                         Set channel name                         |
|    `reset`     |      any       |  Any non-zero-length value will reset light settings to default  |
|    `effect`    |     number     |             Applies an effect, see description below             |
|  `transition`  |     number     | Set transition time between on/off and color change, [0-5000] ms |
|`default_state` |     string     |        Sets default power-on state: `on`, `off` or `last`        |
|   `auto_on`    |     number     |Sets a default timer to turn ON after every OFF command in seconds|
|   `auto_off`   |     number     |Sets a default timer to turn OFF after every ON command in seconds|
|   `btn_type`   |     string     |Input type: `momentary`, `toggle`, `edge`, `detached` or `action` |
| `btn_reverse`  |      bool      |             Whether to invert external switch input              |
|   `schedule`   |      bool      |                      Enable schedule timer                       |
|`schedule_rules`|array of strings|      Rules for schedule activation, e.g. `0000-0123456-on`       |

Supported values for `effect` are:

* `0` - Off
* `1` - Meteor shower
* `2` - Gradual change
* `3` - Flash
* `4` - Red/green change

Shelly RGBW2 Color: `/settings/night_mode`
----------

```

GET /settings/night_mode

{
    "enabled": false,
    "start_time": "00:00",
    "end_time": "00:00",
    "brightness": 20
}

```

When night mode is active, turning ON the device during the set interval it will only go up to the pre-set brightness limit.

### Parameters ###

| Parameter  | Type |                 Description                 |
|------------|------|---------------------------------------------|
| `enabled`  | bool |          Enable/disable night mode          |
|`start_time`|string| Set night mode start time in format `hh:mm` |
| `end_time` |string|  Set night mode end time in format `hh:mm`  |
|`brightness`|number|Set night mode brightness in percent `1..100`|

Shelly RGBW2 Color: `/status`
----------

```

GET /status (in color mode)

{
    "mode": "color",
    "input": 0,
    "lights": [
        {
            "ison": true,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "color",
            "red": 255,
            "green": 127,
            "blue": 0,
            "white": 0,
            "gain": 100,
            "effect": 0,
            "power": 0.46,
            "overpower": false,
            "transition": 500
        }
    ],
    "meters": [
        {
            "power": 0.46,
            "is_valid": true,
            "overpower": false,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ],
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        }
    ]
}

```

### Attributes ###

|Attribute|     Type      |                                                         Description                                                         |
|---------|---------------|-----------------------------------------------------------------------------------------------------------------------------|
| `mode`  |    string     |                                        Currently configured mode, `color` or `white`                                        |
| `input` |    number     |                                                    State of the SW input                                                    |
|`lights` |array of hashes|Contains the current state of the light channels. See [`/color/0`](#shelly-rgbw2-color-color-0) for description of attributes|
|`meters` |array of hashes|                                     Power and energy information, see description below                                     |
|`inputs` |array of hashes|                                     Current state of the inputs, see description below                                      |

### `meters` attributes ###

| Attribute |      Type      |                             Description                             |
|-----------|----------------|---------------------------------------------------------------------|
|  `power`  |     number     |                       Power consumption, `W`                        |
|`is_valid` |      bool      |                Whether power metering self-checks OK                |
|`overpower`|      bool      |             Whether an overpower condition has occured              |
|`timestamp`|     number     |Timestamp of the last energy counter value, with the applied timezone|
|`counters` |array of numbers|  Energy counter value for the last 3 round minutes in Watt-minute   |
|  `total`  |     number     |                Total energy consumed in Watt-minute                 |

### `inputs` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Shelly RGBW2 Color: `/color/0`
----------

```

GET /color/0

{
    "ison": true,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "mode": "color",
    "red": 255,
    "green": 127,
    "blue": 0,
    "white": 0,
    "gain": 100,
    "effect": 0,
    "power": 0.46,
    "overpower": false,
    "transition": 500
}

```

This endpoint controls the output and provides up-to-date state of the device in `color` mode.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                               Whether the output is ON or OFF                                |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|     `mode`      |string|                                  Currently configured mode                                   |
|      `red`      |number|                                   Red brightness, `0..255`                                   |
|     `green`     |number|                                  Green brightness, `0..255`                                  |
|     `blue`      |number|                                  Blue brightness, `0..255`                                   |
|     `white`     |number|                                  White brightness, `0..255`                                  |
|     `gain`      |number|                               Gain for all channels, `0..100`                                |
|    `effect`     |number|                                        Applied effect                                        |
|     `power`     |number|                                     Consumed power, `W`                                      |
|   `overpower`   | bool |                         Whether an overpower condition has occurred                          |
|  `transition`   |number|                             One-shot transition, `0..5000` [ms]                              |

### Parameters ###

| Parameter  | Type |                             Description                             |
|------------|------|---------------------------------------------------------------------|
|  `timer`   |number|Automatic flip-back timer in seconds, used in combination with `turn`|
|   `turn`   |string|              Accepted values: `on`, `off` or `toggle`               |
|   `red`    |number|                      Red brightness, `0..255`                       |
|  `green`   |number|                     Green brightness, `0..255`                      |
|   `blue`   |number|                      Blue brightness, `0..255`                      |
|  `white`   |number|                     White brightness, `0..255`                      |
|   `gain`   |number|                   Gain for all channels, `0..100`                   |
|  `effect`  |number|                          Applies an effect                          |
|`transition`|number|                 One-shot transition, `0..5000` [ms]                 |

Shelly RGBW2 White
==========

Shelly RGBW2 White: Overview
----------

Shelly RGBW2 White is a WiFi-enabled 4-channel 12V/24V LED driver which can control the output channels independently. Via firmware change the same device can be used to control a single RGB+W installation, see [Shelly RGBW2 Color](#shelly-rgbw2-color).

Shelly RGBW2 White supports up to 7 schedule rules.

<https://shelly.cloud/products/shelly-rgbw2-smart-home-automation-led-controller/>

### Factory Reset ###

A factory reset can be performed over the local web interface or Shelly application. In case the device cannot be accessed over network, physical methods for factory reset exist:

* Using the external switch input: turn the device on/off 5 or more times within the first minute after power-on using the switch input terminal. This will trigger a complete factory reset.
* Using the built-in user button:
  * hold for 5 seconds to reset WiFi settings. The device will revert to AP mode.
  * hold for 10 seconds to perform a complete factory reset.

Shelly RGBW2 White: MQTT
----------

```

mosquitto_pub -t shellies/shellyrgbw2-11ABD9/white/2/set \
    -m '{"brightness":70}'

mosquitto_pub -t shellies/shellyrgbw2-11ABD9/white/2/set \
    -m '{"turn":"off","brightness":33}'

```

Shelly RGBW2 White allows for independent control of the 4 output channels with an identical set of MQTT topics. Channels are indexed `0` to `3`.

### Command topics ###

* `shellies/shellyrgbw2-<deviceid>/white/<n>/command` accepts `on` and `off` payloads
* `shellies/shellyrgbw2-<deviceid>/white/<n>/set` accepts a JSON payload with two possible keys:
  * `brightness` sets output level, 0 to 100
  * `turn` can be `on`, `off` or `toggle`, acts just like publishing to `.../command`

```
{
    "brightness": 50,   /* output brightness, 0..100 */
    "turn": "on",       /* "on", "off" or "toggle" */
  "transition": 500   /* One-shot transition, `0..5000` [ms] */
}

```

### Status topics ###

* `shellies/shellyrgbw2-<deviceid>/input/0` reports the current state as `0` or `1`
* `shellies/shellyrgbw2-<deviceid>/longpush/0` reports a value indicating longpush state as `0` (shortpush) or `1` (longpush)
* `shellies/shellyrgbw2-<deviceid>/input_event/0` reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly-rgbw2-white-status) for details

Information about each output channel is published on:

* `shellies/shellyrgbw2-<deviceid>/white/<n>` current on/off state
* `shellies/shellyrgbw2-<deviceid>/white/<n>/status` a JSON payload described below:

```
{
    "ison",             /* whether the output is ON or OFF */
    "has_timer",        /* whether a timer is currently armed for this channel */
    "timer_started",    /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration",   /* timer duration, s */
    "timer_remaining",  /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "mode",             /* "white" */
    "brightness"        /* output brightness, 0..100 */
}

```

Shelly RGBW2 White: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly RGBW2-white SHRGBW2-white](docs/coiot/v2/examples/Shelly%20RGBW2-white%20SHRGBW2-white)

Shelly RGBW2 White: `/settings`
----------

```

GET /settings

{
    "factory_reset_from_switch": true,
    "mode": "white",
    "dcpower": 1,
    "led_status_disable": false,
    "actions": {
        "active": false,
        "names": [
            "btn_on_url",
            "btn_off_url",
            "btn_longpush_url",
            "btn_shortpush_url",
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "name": null,
            "ison": true,
            "brightness": 20,
            "transition": 1000,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "btn_type": "toggle",
            "btn_reverse": 0,
            "schedule_rules": []
        },
        {
            "name": null,
            "ison": true,
            "brightness": 20,
            "transition": 1000,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        },
        {
            "name": null,
            "ison": true,
            "brightness": 20,
            "transition": 1000,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        },
        {
            "name": null,
            "ison": true,
            "brightness": 20,
            "transition": 1000,
            "default_state": "on",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        }
    ],
}

```

### Attributes ###

|         Attribute         |     Type      |                                                              Description                                                              |
|---------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|     bool      |                                 Whether factory reset via 5-time flip of the input switch is enabled                                  |
|          `mode`           |    string     |                                             Currently configured mode, `color` or `white`                                             |
|         `dcpower`         |    number     |                                                  DC supply voltage `0`=12V, `1`=24V                                                   |
|   `led_status_disable`    |     bool      |                                               Whether LED status indication is enabled                                                |
|         `lights`          |array of hashes|         Output channel settings. See [`/settings/white/{index}`](#shelly-rgbw2-white-settings-white-index) for more details.          |
|         `actions`         |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-rgbw2-white-settings-actions)|

3 additional parameters are supported on the `/settings` endpoint for RGBW2 White:

### Parameters ###

|         Parameter         | Type |                                    Description                                     |
|---------------------------|------|------------------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |          Enable/disable factory reset via 5-time flip of the input switch          |
|          `mode`           |string|              Set to `color` or `white`; determines the operating mode              |
|   `led_status_disable`    | bool |                           Disable LED status indication                            |
|         `dcpower`         | bool |               Set to `true` for 24 V power supply, `false` for 12 V                |
|         `actions`         | hash |For setting actions, see [`/settings/actions`](#shelly-rgbw2-white-settings-actions)|

Shelly RGBW2 White: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 2,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 2,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 3,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 3,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly RGBW2 White supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action       |Index|                    Description                    |
|-------------------|-----|---------------------------------------------------|
|   `btn_on_url`    |  0  |   URL to access when input switch is activated    |
|   `btn_off_url`   |  0  |  URL to access when input switch is deactivated   |
|`btn_longpush_url` |  0  |   URL to access when input switch is held down.   |
|`btn_shortpush_url`|  0  |URL to access when input switch is pressed briefly.|
|   `out_on_url`    |  0  |      URL to access when output is activated       |
|   `out_off_url`   |  0  |     URL to access when output is deactivated      |
|   `out_on_url`    |  1  |      URL to access when output is activated       |
|   `out_off_url`   |  1  |     URL to access when output is deactivated      |
|   `out_on_url`    |  2  |      URL to access when output is activated       |
|   `out_off_url`   |  2  |     URL to access when output is deactivated      |
|   `out_on_url`    |  3  |      URL to access when output is activated       |
|   `out_off_url`   |  3  |     URL to access when output is deactivated      |

Shelly RGBW2 White: `/settings/white/{index}`
----------

```

GET /settings/white/0

{
    "name": null,
    "ison": true,
    "brightness": 50,
    "transition": 1000,
    "default_state": "on",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 20
    },
    "btn_type": "toggle",
    "btn_reverse": 0,
    "schedule_rules": [],
    "out_on_url": "",
    "out_off_url": ""
}

```

### Attributes ###

|   Attribute    |      Type      |                                              Description                                               |
|----------------|----------------|--------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                              Channel name                                              |
|     `ison`     |      bool      |                                   Whether the outputs are ON or OFF                                    |
|  `brightness`  |     number     |                                         Output level, `0..100`                                         |
|  `transition`  |     number     |                      Transition time between on/off and white change, [0-5000] ms                      |
|`default_state` |     string     |                                      One of `on`, `off` or `last`                                      |
|   `auto_on`    |     number     |                                          ON-timer value, `s`                                           |
|   `auto_off`   |     number     |                                          OFF-timer value, `s`                                          |
|   `btn_type`   |     string     |                Input type, one of `momentary`, `toggle`, `edge`, `detached` or `action`                |
| `btn_reverse`  |     number     |                           Whether the logical state of the input is inverted                           |
|   `schedule`   |      bool      |                                     Whether scheduling is enabled                                      |
|`schedule_rules`|array of strings|                         Rules for schedule activation, e.g. `0000-0123456-on`                          |
|  `out_on_url`  |     string     |                                 URL to access when output is activated                                 |
| `out_off_url`  |     string     |                                URL to access when output is deactivated                                |
|  `night_mode`  |      hash      |Night mode settings, see [`/settings/light/{index}/night_mode`](#shelly-rgbw2-white-settings-night_mode)|

Each output channel's settings are individually controlled when the device operates in `white` mode with the exception of `btn_type` and `btn_reverse`: they are shared for all channels (and are only visible in `/settings/white/0`)

### Parameters ###

|     Parameter     |      Type      |                           Description                            |
|-------------------|----------------|------------------------------------------------------------------|
|      `name`       |     string     |                         Set channel name                         |
|      `reset`      |      any       |  Any non-zero-length value will reset light settings to default  |
|   `transition`    |     number     | Set transition time between on/off and white change, [0-5000] ms |
|  `default_state`  |     string     |        Sets default power-on state: `on`, `off` or `last`        |
|     `auto_on`     |     number     |Sets a default timer to turn ON after every OFF command in seconds|
|    `auto_off`     |     number     |Sets a default timer to turn OFF after every ON command in seconds|
|    `btn_type`     |     string     |Input type: `momentary`, `toggle`, `edge`, `detached` or `action` |
|   `btn_reverse`   |      bool      |             Whether to invert external switch input              |
|    `schedule`     |      bool      |                      Enable schedule timer                       |
| `schedule_rules`  |array of strings|      Rules for schedule activation, e.g. `0000-0123456-on`       |
|   `btn_on_url`    |     string     |         Set URL to access when input switch is activated         |
|   `btn_off_url`   |     string     |        Set URL to access when input switch is deactivated        |
|`btn_longpush_url` |     string     |         Set URL to access when input switch is held down         |
|`btn_shortpush_url`|     string     |      Set URL to access when input switch is pressed briefly      |
|   `out_on_url`    |     string     |            Set URL to access when output is activated            |
|   `out_off_url`   |     string     |           Set URL to access when output is deactivated           |

Shelly RGBW2 White: `/settings/light/{index}/night_mode`
----------

```

{
    "enabled": false,
    "start_time": "00:00",
    "end_time": "00:00",
    "brightness": 20
}

```

When night mode is active, turning ON the device during the set interval it will only go up to the pre-set brightness limit.

### Parameters ###

| Parameter  | Type |                 Description                 |
|------------|------|---------------------------------------------|
| `enabled`  | bool |          Enable/disable night mode          |
|`start_time`|string| Set night mode start time in format `hh:mm` |
| `end_time` |string|  Set night mode end time in format `hh:mm`  |
|`brightness`|number|Set night mode brightness in percent `1..100`|

Shelly RGBW2 White: `/status`
----------

```

GET /status

{
    "mode": "white",
    "input": 0,
    "total_power": 0,
    "lights": [
        {
            "ison": true,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "white",
            "brightness": 20,
            "transition": 500
        },
        {
            "ison": true,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "white",
            "brightness": 20,
            "transition": 500
        },
        {
            "ison": true,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "white",
            "brightness": 20,
            "transition": 500
        },
        {
            "ison": true,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "white",
            "brightness": 20,
            "transition": 500
        }
    ],
    "meters": [
        {
            "power": 0.46,
            "is_valid": true,
            "overpower": false,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        },
        {
            "power": 0.46,
            "is_valid": true,
            "overpower": false,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        },
        {
            "power": 0.46,
            "is_valid": true,
            "overpower": false,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        },
        {
            "power": 0.46,
            "is_valid": true,
            "overpower": false,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ],
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        }
    ]
}

```

### Attributes ###

|  Attribute  |     Type      |                                                              Description                                                              |
|-------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------|
|   `mode`    |    string     |                                             Currently configured mode, `color` or `white`                                             |
|   `input`   |    number     |                                                         State of the SW input                                                         |
|`total_power`|    number     |                                               Total power consumed by all channels, `W`                                               |
|  `lights`   |array of hashes|Contains the current state of the light channels. See [`/white/{index}`](#shelly-rgbw2-white-white-index) for description of attributes|
|  `meters`   |array of hashes|                                          Power and energy information, see description below                                          |
|  `inputs`   |array of hashes|                                          Current state of the inputs, see description below                                           |

### `meters` attributes ###

| Attribute |      Type      |                             Description                             |
|-----------|----------------|---------------------------------------------------------------------|
|  `power`  |     number     |                       Power consumption, `W`                        |
|`is_valid` |      bool      |                Whether power metering self-checks OK                |
|`overpower`|      bool      |             Whether an overpower condition has occured              |
|`timestamp`|     number     |Timestamp of the last energy counter value, with the applied timezone|
|`counters` |array of numbers|  Energy counter value for the last 3 round minutes in Watt-minute   |
|  `total`  |     number     |                Total energy consumed in Watt-minute                 |

### `inputs` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Shelly RGBW2 White: `/white/{index}`
----------

```

GET /white/0

{
    "ison": true,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "mode": "white",
    "brightness": 20,
    "transition": 500
}

```

This endpoint controls each output channel in `white` mode and can be used for monitoring thereof.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                               Whether the output is ON or OFF                                |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|     `mode`      |string|                                  Currently configured mode                                   |
|  `brightness`   |number|                                 Output brightness, `0..100`                                  |
|  `transition`   |number|                             One-shot transition, `0..5000` [ms]                              |

### Parameters ###

| Parameter  | Type |                             Description                             |
|------------|------|---------------------------------------------------------------------|
|  `timer`   |number|Automatic flip-back timer in seconds, used in combination with `turn`|
|   `turn`   |string|              Accepted values: `on`, `off` or `toggle`               |
|`brightness`|number|           Brightness, `0..100`, applies in `mode="white"`           |
|`transition`|number|                 One-shot transition, `0..5000` [ms]                 |

Shelly Dimmer 1/2
==========

Shelly Dimmer 1/2: Overview
----------

Shelly Dimmer 1/2 is a new smart switch, and this one doesn’t just turn lights on and off, it dims them.
Shelly Dimmer 1/2 can be found on <https://shelly.cloud/products/shelly-dimmer-2-smart-home-light-contoller/>

Shelly Dimmer 1/2 can be used with:

* incandescent and halogen lights: 10-220W
* dimmable LED lights: 50-200VA / 10W-200W
* resistive-inductive loads: ferromagnetic transformers 50-150VA

  * incandescent and halogen lights: 10-220W,
  * dimmable LED lights: 50-200VA / 10W – 200W
  * resistive-inductive loads: ferromagnetic transformers 50-150VA.

Shelly Dimmer SL has the same features as Shelly Dimmer, the only difference being that neutral connection is not required.

Shelly Dimmer and Shelly Dimmer SL supports up to 20 schedule rules.

### Factory Reset ###

* After turning the power on, you have 60 seconds to press 5 consecutive times either switch connected to I1/I2; or
* If you have physical access to the device, press and hold the reset button for 10 seconds. When the LED indicator starts to flash quickly, release the button

Shelly Dimmer 1/2: MQTT
----------

Shelly Dimmer 1/2 allows `on` and `off` commands, as well as brightness:

|                      Topic                       |                                          Description                                          |
|--------------------------------------------------|-----------------------------------------------------------------------------------------------|
|`shellies/shellydimmer-<deviceid>/light/0/command`|                                accepts `on` and `off` payloads                                |
|  `shellies/shellydimmer-<deviceid>/light/0/set`  |accepts a JSON payload in the format `{"brightness": 100, "turn": "on"}`, see description below|

```
{
    "brightness": 100,  /* output brightness 1..100 */
    "turn": "on",       /* one of "on", "off", or "toggle" */
    "transition": 500   /* One-shot transition, `0..5000` [ms] */
}

```

Status information about Shelly Dimmer 1/2 can be accessed on:

|                          Topic                           |                                                                       Description                                                                        |
|----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|       `shellies/shellydimmer-<deviceid>/input/<i>`       |                                             for each SW input `<i>`; reports the current state as `0` or `1`                                             |
|     `shellies/shellydimmer-<deviceid>/longpush/<i>`      |                         for each SW input `<i>`; reports a value indicating longpush state as `0` (shortpush) or `1` (longpush)                          |
|    `shellies/shellydimmer-<deviceid>/input_event/<i>`    |for each SW input `<i>`; reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly-dimmer-1-2-status) for details|
|      `shellies/shellydimmer-<deviceid>/temperature`      |                                                          reports device temperature in Celsius                                                           |
|     `shellies/shellydimmer-<deviceid>/temperature_f`     |                                                         reports device temperature in Fahrenheit                                                         |
|    `shellies/shellydimmer-<deviceid>/overtemperature`    |                                                            reports overtemperature condition                                                             |
|       `shellies/shellydimmer-<deviceid>/overload`        |                                                                reports overload condition                                                                |
|       `shellies/shellydimmer-<deviceid>/loaderror`       |                                                               reports load error condition                                                               |
|        `shellies/shellydimmer-<deviceid>/light/0`        |                                                                  reports on/оff status                                                                   |
|     `shellies/shellydimmer-<deviceid>/light/0/power`     |                                                              reports power consumption, `W`                                                              |
|`shellies/shellydimmer-<deviceid>/light/0/overpower_value`|                                                  Value on which an overpower condition is detected, `W`                                                  |
|    `shellies/shellydimmer-<deviceid>/light/0/energy`     |                                                          reports total energy consumed, `W-min`                                                          |
|    `shellies/shellydimmer-<deviceid>/light/0/status`     |                                                      reports periodic status, see description below                                                      |

```
{
    "ison",            /* whether the channel is turned ON or OFF */
    "has_timer",       /* whether a timer is currently armed for this channel */
    "timer_started",   /* unix timestamp of timer start; 0 if timer inactive or time not synced */
    "timer_duration",  /* timer duration, s */
    "timer_remaining", /* if there is an active timer, shows seconds until timer elapses; 0 otherwise */
    "mode",            /* always `white` */
    "brightness"       /* output brightness, `1..100` */
}

```

Shelly Dimmer 1/2: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Dimmer SHDM-1](docs/coiot/v2/examples/Shelly%20Dimmer%20SHDM-1)

Shelly Dimmer 1/2: `/settings`
----------

```

GET /settings
{
    "factory_reset_from_switch": true,
    "mode": "white",
    "led_status_disable": false,
    "pulse_mode": 0,
    "bypass": true,
    "pulse_mode_detected": false,
    "pulse_mode_rebooted": false,
    "load_autodetect": false,
    "calibrated": false,
    "transition": 0,
    "fade_rate": 0,
    "min_brightness": 20,
    "zcross_debounce": 100,
    "actions": {
        "active": false,
        "names": [
            "btn1_on_url",
            "btn1_off_url",
            "btn1_longpush_url",
            "btn1_shortpush_url",
            "btn2_on_url",
            "btn2_off_url",
            "btn2_longpush_url",
            "btn2_shortpush_url",
            "out_on_url",
            "out_off_url"
        ]
    },
    "lights": [
        {
            "name": null,
            "ison": true,
            "default_state": "off",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": true,
            "night_mode": {
                "enabled": false,
                "start_time": "00:00",
                "end_time": "00:00",
                "brightness": 20
            },
            "schedule_rules": [
                "1720-0123456-120@50%",
                "0000-0123456-123@35%"
                ],
            "btn_type": "edge",
            "btn_debounce": 80,
            "swap_inputs": 0
        }
    ],
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 20
    },
    "warm_up": {
        "enabled": 0,
        "brightness": 0,
        "time": 20
    }
}

```

Shelly Dimmer 1/2 supports only one mode - `white`. It supports a single channel, indexed as `0`.

### Attributes ###

|         Attribute         |     Type      |                                                             Description                                                              |
|---------------------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|     bool      |                                 Whether factory reset via 5-time flip of the input switch is enabled                                 |
|          `mode`           |    string     |                                                      Currently configured mode                                                       |
|   `led_status_disable`    |     bool      |                                               Whether LED status indication is enabled                                               |
|       `pulse_mode`        |    number     |                                       `1` - Leading Edge Dimming, `2` - Trailing Edge Dimming                                        |
|         `bypass`          |     bool      |                                     **Only Dimmer 2** Whether calibration with bypass is enabled                                     |
|   `pulse_mode_detected`   |     bool      |                                           **Only Dimmer 2** Whether pulse mode is detected                                           |
|   `pulse_mode_rebooted`   |     bool      |                                **Only Dimmer 2** Whether device is rebooted during pulse mode detect                                 |
|     `load_autodetect`     |     bool      |                                    **Only Dimmer 2** Whether automatic load detection is enabled                                     |
|       `calibrated`        |     bool      |                                                           Calibration flag                                                           |
|       `transition`        |    number     |                                               Transition time for on/off: `0..5000` ms                                               |
|        `fade_rate`        |    number     |                                        Brightness change speed when button is pressed: `1..5`                                        |
|     `min_brightness`      |    number     |                                                            Min brightness                                                            |
|     `zcross_debounce`     |    number     |                                         Zero-cross (anti-flickering) debounce, microseconds                                          |
|         `actions`         |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-dimmer-1-2-settings-actions)|
|         `lights`          |array of hashes|               Output channel settings, see [`/settings/light/0`](#shelly-dimmer-1-2-settings-light-0) for more details               |
|       `night_mode`        |     hash      |                      Night mode settings, see [`/settings/night_mode`](#shelly-dimmer-1-2-settings-night_mode)                       |
|         `warm_up`         |     hash      |                           Warm up settings, see [`/settings/warm_up`](#shelly-dimmer-1-2-settings-warm_up)                           |

### Parameters ###

|         Parameter         | Type |                                    Description                                    |
|---------------------------|------|-----------------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |         Enable/disable factory reset via 5-time flip of the input switch          |
|   `led_status_disable`    | bool |                           Disable LED status indication                           |
|       `pulse_mode`        |number|              `1` - Leading Edge Dimming, `2` - Trailing Edge Dimming              |
|         `bypass`          | bool |                 **Only Dimmer 2** Enable calibration with bypass                  |
|   `pulse_mode_detected`   | bool |             **Only Dimmer 2** Only accepts `false` to clear the flag              |
|     `load_autodetect`     | bool |             **Only Dimmer 2** Enable/disable automatic load detection             |
|       `transition`        |number|                     Transition time for on/off: `0..5000` ms                      |
|        `fade_rate`        |number|              Brightness change speed when button is pressed: `1..5`               |
|     `min_brightness`      |number|                              Min brightness `0..50`                               |
|     `zcross_debounce`     |number|           Zero-cross (anti-flickering) debounce, `50..150` microseconds           |
|         `actions`         | hash |For setting actions, see [`/settings/actions`](#shelly-dimmer-1-2-settings-actions)|
|        `calibrate`        |number|                 `0` - Delete calibration, `1` - Start calibration                 |
|    `calibrate_cancel`     |number|                             `1` - Cancel calibration                              |

Shelly Dimmer 1/2: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn1_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn1_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn1_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn1_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn2_shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Dimmer 1/2 supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|       Action       |Index|                                            Description                                            |
|--------------------|-----|---------------------------------------------------------------------------------------------------|
|   `btn1_on_url`    |  0  |                             URL to access when SW1 input is activated                             |
|   `btn1_off_url`   |  0  |                            URL to access when SW1 input is deactivated                            |
|`btn1_longpush_url` |  0  |   URL to access when SW1 input is held down. Works only when button is configured as `detached`   |
|`btn1_shortpush_url`|  0  |URL to access when SW1 input is pressed briefly. Works only when button is configured as `detached`|
|   `btn2_on_url`    |  0  |                             URL to access when SW2 input is activated                             |
|   `btn2_off_url`   |  0  |                            URL to access when SW2 input is deactivated                            |
|`btn2_longpush_url` |  0  |   URL to access when SW2 input is held down. Works only when button is configured as `detached`   |
|`btn2_shortpush_url`|  0  |URL to access when SW2 input is pressed briefly. Works only when button is configured as `detached`|
|    `out_on_url`    |  0  |                              URL to access when output is activated                               |
|   `out_off_url`    |  0  |                             URL to access when output is deactivated                              |

Shelly Dimmer 1/2: `/settings/light/0`
----------

```

GET /settings/light/0
{
    "name": null,
    "ison": true,
    "default_state": "off",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": true,
    "night_mode": {
        "enabled": false,
        "start_time": "00:00",
        "end_time": "00:00",
        "brightness": 20
    },
    "schedule_rules": [
        "1720-0123456-120@50%",
        "0000-0123456-123@35%"
        ],
    "btn_type": "edge",
    "btn_debounce": 80,
    "swap_inputs": 0
}

```

### Attributes ###

|   Attribute    |      Type      |                                       Description                                       |
|----------------|----------------|-----------------------------------------------------------------------------------------|
|     `name`     |     string     |                                          Name                                           |
|     `ison`     |      bool      |                                   Dimmer is on or off                                   |
|`default_state` |     string     |              Default power-on state, one of `on`, `off`, `last`, `switch`               |
|   `auto_on`    |     number     |         Default timer to turn the dimmer ON after every OFF command in seconds          |
|   `auto_off`   |     number     |         Default timer to turn the dimmer OFF after every ON command in seconds          |
|   `btn_type`   |     string     | Input type: one of `one_button`, `dual_button`, `toggle`, `edge`, `detached`, `action`  |
| `btn_debounce` |     number     |                               Button debounce time, `ms`                                |
| `swap_inputs`  |      bool      |                                       Swap inputs                                       |
|   `schedule`   |      bool      |                              Whether scheduling is enabled                              |
|  `night_mode`  |      hash      |Night mode settings, see [`/settings/night_mode`](#shelly-dimmer-1-2-settings-night_mode)|
|`schedule_rules`|array of strings|                  Rules for schedule activation, e.g. `0000-0123456-on`                  |

### Parameters ###

|   Parameter    |      Type      |                                      Description                                       |
|----------------|----------------|----------------------------------------------------------------------------------------|
|    `reset`     |      any       |                                 Perform settings reset                                 |
|`default_state` |     string     |              Default power-on state, one of `on`, `off`, `last`, `switch`              |
|   `auto_on`    |     number     |         Default timer to turn the dimmer ON after every OFF command in seconds         |
|   `auto_off`   |     number     |         Default timer to turn the dimmer OFF after every ON command in seconds         |
|   `schedule`   |      bool      |                                Enable scheduling timer                                 |
|`schedule_rules`|array of strings|             String values for sheduling in ir format see description below             |
|   `btn_type`   |     string     |Input type: one of `one_button`, `dual_button`, `toglle`, `edge`, `detached` or `action`|
| `btn_debounce` |     number     |                         Set button debounce time, `60..200ms`                          |
| `swap_inputs`  |      bool      |                                      Swap inputs                                       |

Shelly Dimmer 1/2: `/settings/night_mode`
----------

```

GET /settings/night_mode

{
    "enabled": false,
    "start_time": "00:00",
    "end_time": "00:00",
    "brightness": 20
}

```

When night mode is active, turning ON the device during the set interval it will only go up to the pre-set brightness limit.

### Parameters ###

| Parameter  | Type |                 Description                 |
|------------|------|---------------------------------------------|
| `enabled`  | bool |          Enable/disable night mode          |
|`start_time`|string| Set night mode start time in format `hh:mm` |
| `end_time` |string|  Set night mode end time in format `hh:mm`  |
|`brightness`|number|Set night mode brightness in percent `1..100`|

Shelly Dimmer 1/2: `/settings/warm_up`
----------

```

GET /settings/warm_up

{
    "enabled": 0,
    "brightness": 0,
    "time": 20
}

```

Specify a startup warmup brightness for a short period of time.

### Parameters ###

| Parameter  | Type |                Description                |
|------------|------|-------------------------------------------|
| `enabled`  | bool |          Enable/disable warm up           |
|`brightness`|number|Set warm up brightness in percent `10..100`|
|   `time`   |number|       Set warm up time `20..200ms`        |

Shelly Dimmer 1/2: `/status`
----------

```

GET /status

{
    "lights": [
        {
            "ison": false,
            "source": "http",
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "mode": "white",
            "brightness": 50,
            "transition": 500
        }
    ],
    "meters": [
        {
            "power": 0,
            "overpower": 7.64,
            "is_valid": true,
            "timestamp": 0,
            "counters": [1,2,3],
            "total": 4
        }
    ],
    "inputs": [
        {
            "input": 0,
            "event": "S",
            "event_cnt": 2
        },
        {
            "input": 0,
            "event": "L",
            "event_cnt": 4
        }
    ],
    "tmp": {
        "tC": 50.3,
        "tF": 122.54,
        "is_valid": true
    },
    "calibrated": false,
    "calib_progress": 0,
    "calib_status": 0,
    "calib_running": 0,
    "wire_mode":0,
    "forced_neutral": false,
    "overtemperature": false,
    "loaderror": 0,
    "overload": false
}

```

### Attributes ###

|    Attribute    |     Type      |                                                            Description                                                             |
|-----------------|---------------|------------------------------------------------------------------------------------------------------------------------------------|
|    `lights`     |array of hashes|Contains the current state of the dimmer output channels. See [`/light/0`](#shelly-dimmer-1-2-light-0) for description of attributes|
|    `meters`     |array of hashes|                                     Current status of the power meters, see description below                                      |
|    `inputs`     |array of hashes|                                         Current state of the inputs, see description below                                         |
|    `tmp.tC`     |    number     |                                                      Device temperature in °C                                                      |
|    `tmp.tF`     |    number     |                                                      Device temperature in °F                                                      |
| `tmp.is_valid`  |     bool      |                                                Whether device temperature is valid                                                 |
|  `calibrated`   |     bool      |                                           **Only Dimmer 2** Whether calibration is done                                            |
|`calib_progress` |    number     |                                               Calibration progress, `0..100` percent                                               |
| `calib_status`  |    number     |                                  **Only Dimmer 2** `0` - OK, `1` - DCHI error, `2` - power error                                   |
| `calib_running` |    number     |                                          **Only Dimmer 2** Whether calibration is running                                          |
|   `wire_mode`   |    number     |                                           **Only Dimmer 2** `0` - LO mode, `1` - LN mode                                           |
|`forced_neutral` |     bool      |                                               **Only Dimmer 2** Forced neutral flag                                                |
|`overtemperature`|     bool      |                                         Whether an overtemperature condition has occurred                                          |
|   `loaderror`   |    number     |                                                             Load error                                                             |
|   `overload`    |     bool      |                                             Whether an overload condition has occurred                                             |

### `meters` attributes ###

| Attribute |      Type      |                             Description                             |
|-----------|----------------|---------------------------------------------------------------------|
|  `power`  |     number     |                 Current power being drawn, in Watts                 |
|`overpower`|     number     |     Value in Watts, on which an overpower condition is detected     |
|`is_valid` |      bool      |                Whether power metering self-checks OK                |
|`timestamp`|     number     |Timestamp of the last energy counter value, with the applied timezone|
|`counters` |array of numbers|  Energy counter value for the last 3 round minutes in Watt-minute   |
|  `total`  |     number     |                Total energy consumed in Watt-minute                 |

### `inputs.{index}` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                Current state of the input `0/1`                |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON. `event` provides a short string, designating the last detected input event (shortpush/longpush). `event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Shelly Dimmer 1/2: `/light/0`
----------

```

GET /light/0

{
    "ison": false,
    "source": "http",
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "mode": "white",
    "brightness": 50,
    "transition": 500
}

```

This endpoint allows sending commands to the dimmer to control it.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|    `source`     |string|                                  Source of the last command                                  |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|     `mode`      |string|                                        Always `white`                                        |
|  `brightness`   |number|                                 Output brightness, `1..100`                                  |
|  `transition`   |number|                             One-shot transition, `0..5000` [ms]                              |

### Parameters ###

| Parameter  | Type |                         Description                          |
|------------|------|--------------------------------------------------------------|
|  `timer`   |number|            A one-shot flip-back timer in seconds             |
|   `turn`   |string|           Command to turn `on`, `off` or `toggle`            |
|`brightness`|number|                     Brightness, `1..100`                     |
|`transition`|number|             One-shot transition, `0..5000` [ms]              |
|   `dim`    |string|      Dimming direction, accepts `up`, `down` or `stop`       |
|   `step`   |number|Dimming step in [%]; Used in ccombination with `dim` parameter|

Shelly Sense
==========

Shelly Sense: Overview
----------

Shelly Sense is the most advanced Wi-Fi Room sensor and universal IR control on the market today. Shelly Sense has:

* 360° infrared transmission and can control any air conditioner, TV and Hi-Fi set
* Temperature sensor
* Humidity sensor
* LUX/Light sensor
* Motion sensor
* 4400mAh battery

Shelly Sense can operate up to 10 days on the battery.

The settings of Shelly Sense can be changed via the [`/settings`](#shelly-sense-settings) endpoint. Commands to perform actions can come from:

* Physical buttons
* HTTP request, trough the local web interface
* A command sent via the cloud
* A weekly-schedule event

### Factory Reset ###

|If the web interface of the device cannot be accessed, settings can be brought back to defaults by pressing and holding the setup button for more then 10 seconds or until the red LED light start flashing fast.|
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                   Factory reset will remove all added IR codes and schedules from the device.                                                                   |

Shelly Sense: MQTT
----------

Shelly Sense sends values from its internal sensors on the following topics:

|                       Topic                        |                     Description                      |
|----------------------------------------------------|------------------------------------------------------|
|  `shellies/shellysense-<deviceid>/sensor/motion`   |  `true` when motion is detected, `false` otherwise   |
|  `shellies/shellysense-<deviceid>/sensor/charger`  |Whether external power is available, `true` or `false`|
|`shellies/shellysense-<deviceid>/sensor/temperature`|        In °C or °F depending on configuration        |
| `shellies/shellysense-<deviceid>/sensor/humidity`  |                       RH in %                        |
|    `shellies/shellysense-<deviceid>/sensor/lux`    |                  Illuminance in Lux                  |
|  `shellies/shellysense-<deviceid>/sensor/battery`  |                  Battery level in %                  |

Shelly Sense: `/settings`
----------

The settings for Shelly Sense are:

* Motion duration time (sec) - how long Shelly Sense will keep the motion flag after motion detection
* Motion LED indication - disable and enable the LED light which indicates motion detection status
* Temperature units - Celsius or Fahrenheit

```
GET /settings/
{
    "light_sensor": "NOA1305",
    "schedule": false,
    "schedule_rules": [],
    "sensors": {
        "motion_duration": 20,
        "motion_led": true,
        "temperature_unit": "C"
    }
}

```

### Attributes ###

|        Attribute         |      Type      |                          Description                          |
|--------------------------|----------------|---------------------------------------------------------------|
|      `light_sensor`      |     string     |                    Light sensor type name                     |
|        `schedule`        |      bool      |                Schedule timer enabled/disabled                |
|     `schedule_rules`     |array of strings|                Definition of scheduling rules                 |
|`sensors.motion_duration` |     number     |Duration time in seconds for motion flag after motion detection|
|   `sensors.motion_led`   |      bool      |       Whether LED light should indicate motion detected       |
|`sensors.temperature_unit`|     string     |   Temperature units: `C` for Celsius and `F` for Fahrenheit   |

### Parameters ###

|        Parameter         |      Type      |                            Description                            |
|--------------------------|----------------|-------------------------------------------------------------------|
|   `temperature_units`    |     string     |   Set temperature units: `C` for Celsius and `F` for Fahrenheit   |
|`pir_motion_duration_time`|     number     |Set duration time in seconds for motion flag after motion detection|
|     `pir_motion_led`     |      bool      |       Set whether LED light should indicate motion detected       |
|        `schedule`        |      bool      |                  Enable/disable scheduling timer                  |
|     `schedule_rules`     |array of strings|       Add or Remove weekly schedule. See description below        |

### Shelly Sense Schedule: `/settings/?schedule` ###

Shelly Sense can send IR codes automatically by predefined weekly schedule.
Before adding schedule rules, IR codes must be stored in the device (see [`/ir/add`](#shelly-sense-ir-add) and [`/ir/list`](#shelly-sense-ir-list))

### Parameters ###

|   Parameter    |      Type      |         Description         |
|----------------|----------------|-----------------------------|
|   `schedule`   |      bool      |Activate/Deactivate schedules|
|`schedule_rules`|array of strings|     Set schedule rules      |

### Shelly Sense Schedule rules: `/settings/?schedule_rules` ###

A schedule rule is a string that contains:

|Value| Range |                            Description                             |
|-----|-------|--------------------------------------------------------------------|
| ET  |  24h  |                  Executing time in format `HHMM`                   |
| WD  |0123456|Days of week on which schedule will be executed starting from Monday|
| ID  |       |                 ID of the stored pronto code (ID)                  |

These variables should be concatenated with `-`. If you want to add more schedules then use `,` between each of them.
The final string should look like:

schedule\_rules=`ET-WD-ID`,`ET-WD-ID`

The schedule is set as whole set. Every time you want to add a new rule, you should append old ones too.

### Examples ###

|Description|                                         Example                                          |
|-----------|------------------------------------------------------------------------------------------|
|Set Shedule|`http://localIP/settings/?schedule_rules=1734-012-ir0_17_1_0_0_25,1222-0123456-ir1_41_pwr`|

Shelly Sense: `/status`
----------

```
GET /status
{
    "motion": false,
    "charger": false,
    "tmp": {
        "value": 9.55536,
        "is_valid": true,
        "units": "C"
    },
    "hum": {
        "value": 85.548308,
        "is_valid": true,
    },
    "lux":{
        "value": 3.896104,
        "is_valid": true,
    },
    "bat":{
        "value": 100
    }
}

```

Shelly Sense `status` command gives information about the device and all sensors status.

* Motion status
* Charging status
* Battery level %
* Temperature information
* Humidity information
* Brightness information in lux

### Attributes ###

|Attribute|Type|      Description      |
|---------|----|-----------------------|
|`motion` |bool|   Motion detection    |
|`charger`|bool|    Charging status    |
|  `tmp`  |hash|Temperature information|
|  `hum`  |hash| Humidity information  |
|  `lux`  |hash|Brightness information |
|  `bat`  |hash|     Battery level     |

Shelly Sense: `/ir`
----------

To preset IR codes in your Shelly Sense you should use Shelly Cloud application from [iOS](https://itunes.apple.com/si/app/shelly-cloud/id1147141552?mt=8) or [Android](https://play.google.com/store/apps/details?id=allterco.bg.shelly) store.
These apps provide access to a huge database for TV, Hi-Fi sets and air conditioners. Any IR code can be added to Shelly Sense in "pronto" format so you can command your exotic IR operated devices.

### Parameters ###

|Parameter| Type |                                        Description                                         |
|---------|------|--------------------------------------------------------------------------------------------|
| `list`  |string|                      List for stored infrared devices in Shelly Sense                      |
|  `add`  |string|Add new device into Shelly Sense. For more information see [`/ir/add`](#shelly-sense-ir-add)|
|`remove` |string|Remove IR code or device stored in Shelly Sense. See [`/ir/remove`](#shelly-sense-ir-remove)|
| `emit`  |string|           Send IR code from Shelly Sens. See [`/ir/emit`](#shelly-sense-ir-emit)           |

Shelly Sense: `/ir/list`
----------

Here is a sample list of stored IR codes in Shelly Sense for TV and Air-conditioning.

```
 GET /ir/list
[
    [
        "1_41_pwr",
        "TV Philips(41) - Power"
    ],
    ]
        "0_17_1_0_0_25",
        ":;8<0 (17) - Turn on, Mode: AUTO, Fan: AUTO, Temp: 25"
    ],
]

```

### Attributes ###

|Attribute| Type |                  Description                  |
|---------|------|-----------------------------------------------|
|  `ID`   |string|  ID of the stored IR code into Shelly Sense   |
| `name`  |string|Short description or name of the stored IR code|

Shelly Sense: `/ir/add`
----------

You can add base64 encoded pronto code into Shelly Sense and send it by ID.

```
 GET /ir/add?

```

### Parameters ###

|Parameter| Type |                  Description                  |
|---------|------|-----------------------------------------------|
|  `ID`   |string|               ID of the IR code               |
| `name`  |string|Short description or name of the stored IR code|
|`pronto` |string|             IR pronto code base64             |

Shelly Sense: `/ir/remove`
----------

Shelly Sense API support few ways to remove codes:

* only one IR code by ID
* pronto codes by prefix of ID
* all pronto codes

```

 GET /ir/remove?

```

### Parameters ###

|Parameter| Type |               Description                |
|---------|------|------------------------------------------|
|  `ID`   |string|ID of the stored IR code into Shelly Sense|
|  `all`  |string|Remove all pronto codes from Shelly Sense |
|`prefix` |string|      Remove pronto codes by prefix       |

### Examples ###

|  Description   |                                           Example                                            |
|----------------|----------------------------------------------------------------------------------------------|
|  Remove by ID  |                           `http://localIP/ir/remove?id=1_91_chdwn`                           |
|   Remove all   |                               `http://localIP/ir/remove?all=1`                               |
|Remove by prefix|                            `http://localIP/ir/remove?prefix=1_91`                            |
|     Add IR     |`http://localIP/ir/add?id=1_91_chdwn&name=tv(91)%20-%20Channel%20Down&pronto=AAAAbQAiAAIBV...`|

Shelly Sense: `/ir/emit`
----------

You can send IR code from Shelly Sense using:

* Stored pronto code in Shelly Sense. See [`/ir/add`](#shelly-sense-ir-add)
* Base64 encoded pronto code
* HEX pronto code

```

 GET /ir/emit

```

### Parameters ###

| Parameter  | Type |                     Description                      |
|------------|------|------------------------------------------------------|
|   `type`   |string|Type of IR code you want to send: `stored` or `pronto`|
|    `ID`    |string| Send stored pronto code by ID when `type` = `stored` |
|  `pronto`  |string|Send Base64 encoded pronto code when `type` = `pronto`|
|`pronto_hex`|string| Send HEX encoded pronto code when `type` = `pronto`  |

Shelly H&T
==========

Shelly H&T: Overview
----------

Shelly H&T is a WiFi humidity and temperature sensor with long battery life:

<https://shelly.cloud/products/shelly-humidity-temperature-smart-home-automation-sensor/>

Shelly H&T normally keeps its WiFi controller shut down and only wakes up when an update is due. This can either be a periodic wakeup or sensor reading change greater than the configured threshold. On these events, the device wakes up to report updated sensor values and shuts back down immediately afterwards.

When the user button is pressed, the device switches to a "setup" mode -- it will remain turned on for 3 minutes, allowing configuration over the web interface. Another short button press will put it back to sleep.

### Factory Reset ###

To restore Shelly H&T to its factory settings, turn the device on if needed, then press and hold the user button until the LED stops blinking rapidly.

Shelly H&T: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly H&T sends values from its internal sensors on the following topics:

* `shellies/shellyht-<deviceid>/sensor/temperature`: in °C or °F depending on configuration
* `shellies/shellyht-<deviceid>/sensor/humidity`: RH in %
* `shellies/shellyht-<deviceid>/sensor/battery`: battery level in %
* `shellies/shellyht-<deviceid>/sensor/error`: if different from `0`, there is an error with the sensor
* `shellies/shellyht-<deviceid>/sensor/act_reasons`: list of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `alarm`
* `shellies/shellyht-<deviceid>/sensor/ext_power`: `true`, if the device is usb powered

Shelly H&T: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly H\_T SHHT-1](docs/coiot/v2/examples/Shelly%20H_T%20SHHT-1)

Shelly H&T: `/settings`
----------

```
GET /settings

{
    "device": {
        "sleep_mode": true
    },
    "actions": {
        "active": false,
        "names": [
            "report_url",
            "temp_over_url",
            "temp_under_url",
            "hum_over_url",
            "hum_under_url"
        ]
    },
    "sensors": {
        "temperature_threshold": 1,
        "temperature_unit": "C",
        "humidity_threshold": 5
    },
    "sleep_mode": {
        "period": 12,
        "unit": "h"
    },
    "external_power": 0,
    "temperature_offset": 0,
    "humidity_offset": 0
}

```

### Attributes ###

|           Attribute           | Type |                                                            Description                                                            |
|-------------------------------|------|-----------------------------------------------------------------------------------------------------------------------------------|
|      `device.sleep_mode`      | bool |                                                           Always `true`                                                           |
|           `actions`           | hash |  List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-h-t-settings-actions)  |
|`sensors.temperature_threshold`|number|                                        Temperature delta (in °C) which triggers an update                                         |
|  `sensors.temperature_unit`   |string|                                                         Either `C` or `F`                                                         |
| `sensors.humidity_threshold`  |number|                                          Humidity delta (in %) which triggers an update                                           |
|      `sleep_mode.period`      |number|Periodic update period in `sleep_mode.unit`, depends on `external_power` (`12h` if `external_power=0`, `10m` if `external_power=1`)|
|       `sleep_mode.unit`       |string|                                                            `m` or `h`                                                             |
|       `external_power`        |number|                                            Whether external power supply is installed                                             |
|     `temperature_offset`      |number|                                                    Temperature offset (in °C)                                                     |
|       `humidity_offset`       |number|                                                      Humidity offset (in %)                                                       |

Shelly HT accepts the following extra parameters on it's `/settings` endpoint:

### Parameters ###

|       Parameter       | Type |                                Description                                 |
|-----------------------|------|----------------------------------------------------------------------------|
|       `actions`       | hash |For setting actions, see [`/settings/actions`](#shelly-h-t-settings-actions)|
|  `temperature_units`  |string|                             Either `C` or `F`                              |
|`temperature_threshold`|number|        Temperature delta (in °C) which triggers an update, `0..15`         |
| `humidity_threshold`  |number|          Humidity delta (in %) which triggers an update, `0..100`          |
|   `external_power`    | bool |                 Set if external power supply is installed                  |
| `temperature_offset`  |number|                   Temperature offset (in °C), `-50..50`                    |
|   `humidity_offset`   |number|                     Humidity offset (in %), `-50..50`                      |

Shelly H&T: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "report_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "temp_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "temp_over_value": 21.5,
        "temp_over_onetime": true
      }
    ],
    "temp_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "temp_under_value": 19.7,
        "temp_under_onetime": false
      }
    ],
    "hum_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "hum_over_value": 60,
        "hum_over_onetime": true
      }
    ],
    "hum_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "hum_under_value": 40,
        "hum_under_onetime": false
      }
    ]
  }
}

```

### Actions ###

Shelly H&T supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|     Action     |Index|                               Description                               |
|----------------|-----|-------------------------------------------------------------------------|
|  `report_url`  |  0  |URL to report sensor events on (`/?hum=60&temp=25.00&id=shellyht-xxxxxx`)|
|`temp_over_url` |  0  |           URL to invoke when temperature \> `temp_over_value`           |
|`temp_under_url`|  0  |          URL to invoke when temperature \< `temp_under_value`           |
| `hum_over_url` |  0  |             URL to invoke when humidity \> `hum_over_value`             |
|`hum_under_url` |  0  |            URL to invoke when humidity \< `hum_under_value`             |

### Additional parameters ###

|     Parameter      | Type |                             Description                              |
|--------------------|------|----------------------------------------------------------------------|
| `temp_over_value`  |number|          Temperature over which to trigger `temp_over_url`           |
|`temp_over_onetime` | bool |Whether the `temp_over_url` will be triggered repeatedly or only once |
| `temp_under_value` |number|         Temperature under which to trigger `temp_under_url`          |
|`temp_under_onetime`| bool |Whether the `temp_under_url` will be triggered repeatedly or only once|
|  `hum_over_value`  |number|            Humidity over which to trigger `hum_over_url`             |
| `hum_over_onetime` | bool | Whether the `hum_over_url` will be triggered repeatedly or only once |
| `hum_under_value`  |number|           Humidity under which to trigger `hum_under_url`            |
|`hum_under_onetime` | bool |Whether the `hum_under_url` will be triggered repeatedly or only once |

Shelly H&T: `/status`
----------

```
GET /status

{
    "is_valid": true,
    "tmp": {
        "value": 22,
        "units": "C",
        "tC": 22,
        "tF": 71.6,
        "is_valid": true
    },
    "hum": {
        "value": 57,
        "is_valid": true
    },
    "bat": {
        "value": 71,
        "voltage": 2.73
    },
    "act_reasons": [
        "button"
    ],
    "connect_retries": 0
}

```

Sensor values are repoted on the `/status` endpoint, along with info on the reason the device is awake.

### Attributes ###

|    Parameter    |      Type      |                                              Description                                              |
|-----------------|----------------|-------------------------------------------------------------------------------------------------------|
|   `is_valid`    |      bool      |                                   Whether ht sensor self-checks OK                                    |
|   `tmp.value`   |     number     |                                    Temperature in configured units                                    |
|   `tmp.units`   |     string     |                                              `C` or `F`                                               |
|    `tmp.tC`     |     number     |                                           Temperature in °C                                           |
|    `tmp.tF`     |     number     |                                           Temperature in °F                                           |
| `tmp.is_valid`  |      bool      |                           Whether the internal sensor is operating properly                           |
|   `hum.value`   |     number     |                                        Relative humidity in %                                         |
| `hum.is_valid`  |      bool      |                           Whether the internal sensor is operating properly                           |
|   `bat.value`   |     number     |                          Estimated remaining battery capacity in %, `0..100`                          |
|  `bat.voltage`  |     number     |                                         Battery voltage, `V`                                          |
|  `act_reasons`  |array of strings|List of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `alarm`|
|`connect_retries`|     number     |                                         WiFi connect retries                                          |
| `sensor_error`  |     number     |                                    Only displayed in case of error                                    |

Shelly Smoke
==========

Shelly Smoke: Overview
----------

Shelly Smoke is a WiFi temperature sensor and fire detector with long battery life:

<https://shelly.cloud/products/shelly-smoke-smart-home-automation-sensor/>

Shelly Smoke normally keeps its WiFi controller shut down and only goes online when an update is due. This can either be a periodic wakeup, low battery condition, temperature reading change greater than the configured threshold or, hopefully not, a fire. On these events, the device wakes up to report updated sensor values and shuts back down. In the case of a fire alarm, the sensor will keep alarming until the smoke clears up or it's battery dies.

When the user button is pressed, the device switches to a "setup" mode -- it will remain turned on for 3 minutes, allowing configuration over the web interface. Another short button press will put it back to sleep.

### Factory Reset ###

To restore Shelly Smoke to its factory settings, turn the device on if needed, then press and hold the user button until the LED stops blinking rapidly.

Shelly Smoke: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly Smoke sends values from its internal sensors on the following topics:

* `shellies/shellysmoke-<deviceid>/sensor/temperature`: in °C or °F depending on configuration
* `shellies/shellysmoke-<deviceid>/sensor/smoke`: whether presence of smoke was detected, `true` or `false`
* `shellies/shellysmoke-<deviceid>/sensor/battery`: battery level in %

Shelly Smoke: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Smoke SHSM-01](docs/coiot/v2/examples/Shelly%20Smoke%20SHSM-01)

Shelly Smoke: `/settings`
----------

```
GET /settings

{
    "device": {
        "sleep_mode": true
    },
    "actions": {
        "active": false,
        "names": [
            "fire_detected_url",
            "fire_gone_url"
        ]
    },
    "sensors": {
        "temperature_threshold": 1,
        "temperature_unit": "C",
    },
    "sleep_mode": {
        "period": 12,
        "unit": "h"
    },
    "temperature_offset": 0
}

```

### Attributes ###

|           Attribute           | Type |                                                           Description                                                           |
|-------------------------------|------|---------------------------------------------------------------------------------------------------------------------------------|
|      `device.sleep_mode`      | bool |                                                          Always `true`                                                          |
|           `actions`           | hash |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-smoke-settings-actions)|
|`sensors.temperature_threshold`|number|                                       Temperature delta (in °C) which triggers an update                                        |
|  `sensors.temperature_unit`   |string|                                                        Either `C` or `F`                                                        |
|      `sleep_mode.period`      |number|                                          Periodic update period in hours, always `12`                                           |
|       `sleep_mode.unit`       |string|                                                           Always `h`                                                            |
|     `temperature_offset`      |number|                                                   Temperature offset (in °C)                                                    |

Shelly Smoke accepts the following extra parameters on its `/settings` endpoint:

### Parameters ###

|       Parameter       | Type |                                 Description                                  |
|-----------------------|------|------------------------------------------------------------------------------|
|       `actions`       | hash |For setting actions, see [`/settings/actions`](#shelly-smoke-settings-actions)|
|  `temperature_units`  |string|                              Either `C` or `F`                               |
|`temperature_threshold`|number|         Temperature delta (in °C) which triggers an update, `0..15`          |
| `temperature_offset`  |number|                    Temperature offset (in °C), `-50..50`                     |

Shelly Smoke: `/settings/actions`
----------

```

GET /settings/actions
{
  "actions": {
    "fire_detected_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "fire_gone_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Smoke supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|      Action       |Index|                      Description                       |
|-------------------|-----|--------------------------------------------------------|
|`fire_detected_url`|  0  |     URL to access when fire condition is detected      |
|  `fire_gone_url`  |  0  |URL to access when fire condition is not present anymore|

Shelly Smoke: `/status`
----------

```
GET /status

{
    "is_valid": true,
    "smoke": false,
    "tmp": {
        "value": 22,
        "units": "C",
        "tC": 22,
        "tF": 71.6,
        "is_valid": true
    },
    "bat": {
        "value": 71,
        "voltage": 2.73
    },
    "act_reasons": [
        "button"
    ]
}

```

Sensor values are repoted on the `/status` endpoint, along with info on the reason the device is awake.

### Attributes ###

|  Parameter   |      Type      |                                                          Description                                                          |
|--------------|----------------|-------------------------------------------------------------------------------------------------------------------------------|
|  `is_valid`  |      bool      |                                              Whether smoke sensor self-checks OK                                              |
|   `smoke`    |      bool      |                                                   Wheter smoke is detected                                                    |
| `tmp.value`  |     number     |                                               Temperature in configured unites                                                |
| `tmp.units`  |     string     |                                                          `C` or `F`                                                           |
|   `tmp.tC`   |     number     |                                                       Temperature in °C                                                       |
|   `tmp.tF`   |     number     |                                                       Temperature in °F                                                       |
|`tmp.is_valid`|      bool      |                                 Whether the internal temperature sensor is operating properly                                 |
| `bat.value`  |     number     |                                      Estimated remaining battery capacity in %, `0..100`                                      |
|`bat.voltage` |     number     |                                                     Battery voltage, `V`                                                      |
|`act_reasons` |array of strings|List of reasons which woke up the device, may contain either of: `battery`, `button`, `periodic`, `poweron`, `sensor`, `alarm`.|
|`sensor_error`|     number     |                                                Only displayed in case of error                                                |

Shelly Flood
==========

Shelly Flood: Overview
----------

Shelly Flood is a WiFi-connected water-leak sensor.

[Product page](https://shelly.cloud/products/shelly-flood-smart-home-automation-sensor/)

Shelly Flood normally keeps its WiFi controller shut down and only wakes up when an update is due or an event needs to be reported. On these events, the device wakes up to report updated sensor values and shuts back down immediately afterwards.

When the user button is pressed, the device switches to a "setup" mode -- it will remain turned on for 3 minutes, allowing configuration over the web interface. Another short button press will put it back to sleep.

When Rain Mode is enabled, the device will not raise any alarms when water is detected. Instead, it will just report the event and go back to sleep. Another event update will be sent when the water clears.

### Factory Reset ###

To restore Shelly Flood to its factory settings:

* turn the device on, either by re-inserting the battery or pressing the button shortly; then press and hold the built-in user button for more than 10 seconds.

Shelly Flood: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly Flood sends values from its internal sensors on the following topics:

* `shellies/shellyflood-<deviceid>/sensor/battery`: battery level in %
* `shellies/shellyflood-<deviceid>/sensor/flood`: reports `true` when flood is detected, `false` otherwise
* `shellies/shellyflood-<deviceid>/sensor/temperature`: in °C or °F depending on configuration
* `shellies/shellyflood-<deviceid>/sensor/error`: if different from `0`, there is an error with the sensor
* `shellies/shellyflood-<deviceid>/sensor/act_reasons`: list of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `alarm`

Shelly Flood: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Flood SHWT-1](docs/coiot/v2/examples/Shelly%20Flood%20SHWT-1)

Shelly Flood: `/settings`
----------

```
GET /settings

{
    "device": {
        "sleep_mode": true
    },
    "actions": {
        "active": false,
        "names": [
            "report_url",
            "flood_detected_url",
            "flood_gone_url",
            "temp_over_url",
            "temp_under_url"
        ]
    },
    "sensors": {
        "temperature_threshold": 1,
        "temperature_unit": "C"
    },
    "sleep_mode": {
        "period": 12,
        "unit": "h"
    },
    "rain_sensor": false,
    "temperature_offset": 0
}

```

### Attributes ###

|           Attribute           | Type |                                                           Description                                                           |
|-------------------------------|------|---------------------------------------------------------------------------------------------------------------------------------|
|      `device.sleep_mode`      | bool |                                                          Always `true`                                                          |
|           `actions`           | hash |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-flood-settings-actions)|
|`sensors.temperature_threshold`|number|                                       Temperature delta (in °C) which triggers an update                                        |
|  `sensors.temperature_unit`   |string|                                                        Either `C` or `F`                                                        |
|      `sleep_mode.period`      |number|                                                 Periodic update period in hours                                                 |
|       `sleep_mode.unit`       |string|                                                           Always `h`                                                            |
|         `rain_sensor`         | bool |                           Whether Rain Mode is enabled (no buzzer and report only when water changes)                           |
|     `temperature_offset`      |number|                                                   Temperature offset (in °C)                                                    |

Shelly Flood accepts the following extra parameters on it's `/settings` endpoint:

### Parameters ###

|       Parameter       | Type |                                 Description                                  |
|-----------------------|------|------------------------------------------------------------------------------|
|       `actions`       | hash |For setting actions, see [`/settings/actions`](#shelly-flood-settings-actions)|
|  `temperature_units`  |string|                              Either `C` or `F`                               |
|`temperature_threshold`|number|         Temperature delta (in °C) which triggers an update, `0..15`          |
|     `rain_sensor`     | bool |   Enable/disable Rain Mode (no buzzer and report only when water changes)    |
| `temperature_offset`  |number|                    Temperature offset (in °C), `-50..50`                     |

Shelly Flood: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "report_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "flood_detected_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "flood_gone_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "temp_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "temp_over_value": 21.5,
        "temp_over_onetime": true
      }
    ],
    "temp_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "temp_under_value": 19.7,
        "temp_under_onetime": false
      }
    ]
  }
}

```

### Actions ###

Shelly Flood supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|       Action       |Index|                                      Description                                      |
|--------------------|-----|---------------------------------------------------------------------------------------|
|    `report_url`    |  0  |URL to report sensor events on (`/?temp=25.00&flood=0&batV=1.00&id=shellyflood-xxxxxx`)|
|`flood_detected_url`|  0  |                         URL to access when flood is detected                          |
|  `flood_gone_url`  |  0  |                           URL to access when flood is gone                            |
|  `temp_over_url`   |  0  |                  URL to invoke when temperature \> `temp_over_value`                  |
|  `temp_under_url`  |  0  |                 URL to invoke when temperature \< `temp_under_value`                  |

### Additional parameters ###

|     Parameter      | Type |                             Description                              |
|--------------------|------|----------------------------------------------------------------------|
| `temp_over_value`  |number|          Temperature over which to trigger `temp_over_url`           |
|`temp_over_onetime` | bool |Whether the `temp_over_url` will be triggered repeatedly or only once |
| `temp_under_value` |number|         Temperature under which to trigger `temp_under_url`          |
|`temp_under_onetime`| bool |Whether the `temp_under_url` will be triggered repeatedly or only once|

Shelly Flood: `/status`
----------

```
GET /status

{
    "is_valid": true,
    "flood": false,
    "tmp": {
        "value": 20,
        "units": "C",
        "tC": 20,
        "tF": 68,
        "is_valid": true
    },
    "bat": {
        "value": 71,
        "voltage": 2.73
    },
    "act_reasons": [
        "periodic"
    ],
    "rain_sensor": false
}

```

### Attributes ###

|  Parameter   |      Type      |                                              Description                                              |
|--------------|----------------|-------------------------------------------------------------------------------------------------------|
|  `is_valid`  |      bool      |                                  Whether flood sensor self-checks OK                                  |
|   `flood`    |      bool      |                                 Wheter a flood condition is detected                                  |
| `tmp.value`  |     number     |                                    Temperature in configured units                                    |
| `tmp.units`  |     string     |                                              `C` or `F`                                               |
|   `tmp.tC`   |     number     |                                           Temperature in °C                                           |
|   `tmp.tF`   |     number     |                                           Temperature in °F                                           |
|`tmp.is_valid`|      bool      |                     Whether the internal temperature sensor is operating properly                     |
| `bat.value`  |     number     |                          Estimated remaining battery capacity in %, `0..100`                          |
|`bat.voltage` |     number     |                                         Battery voltage, `V`                                          |
|`act_reasons` |array of strings|List of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `alarm`|
|`rain_sensor` |      bool      |              Whether Rain Mode is enabled (no buzzer and report only when water changes)              |
|`sensor_error`|     number     |                                    Only displayed in case of error                                    |

Shelly Door/Window 1/2
==========

Shelly Door/Window 1/2: Overview
----------

Shelly Door/Window 2 is a WiFi-connected door and window sensor with lux measurement.

[Product page](https://shelly.cloud/products/shelly-door-window-2-smart-home-automation-sensor/)

### Factory Reset ###

To restore Shelly Door/Window 1/2 to its factory settings:

* turn the device on, either by re-inserting the battery or pressing the button shortly; then press and hold the built-in user button for more than 10 seconds.

Shelly Door/Window 1/2: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly Door/Window sends values from its internal sensors on the following topics:

* `shellies/shellydw-<deviceid>/sensor/state`: door/window sensor state `open` or `close`
* `shellies/shellydw-<deviceid>/sensor/tilt`: tilt in °, `0..180`
* `shellies/shellydw-<deviceid>/sensor/vibration`: `0` - no vibration, `1` - vibration detected
* `shellies/shellydw-<deviceid>/sensor/lux`: luminance level in `lux`
* `shellies/shellydw-<deviceid>/sensor/battery`: battery level in %
* `shellies/shellydw-<deviceid>/sensor/temperature`: **Door/Window 2 only** Temperature, in `C` or `F` as per user configuration
* `shellies/shellydw-<deviceid>/sensor/error`: if different from `0`, there is an error with the sensor
* `shellies/shellydw-<deviceid>/sensor/act_reasons`: list of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `movement`, `temperature`, `light`

Shelly Door/Window 1/2: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Door Window SHDW-1](docs/coiot/v2/examples/Shelly%20Door%20Window%20SHDW-1)
* [Shelly Door Window 2 SHDW-2](docs/coiot/v2/examples/Shelly%20Door%20Window%202%20SHDW-2)

Shelly Door/Window 1/2: `/settings`
----------

```
GET /settings (for Door/Window 2)

{
    "device": {
        "sleep_mode": true
    },
    "actions": {
        "active": false,
        "names": [
            "report_url",
            "dark_url",
            "twilight_url",
            "open_url",
            "close_url",
            "vibration_url",
            "temp_over_url",
            "temp_under_url"
        ]
    },
    "dark_threshold": 100,
    "twilight_threshold": 300,
    "sleep_mode": {
        "period": 6,
        "unit": "h"
    },
    "led_status_disable": true,
    "lux_wakeup_enable": false,
    "tilt_enabled": false,
    "tilt_calibrated": false,
    "vibration_enabled": false,
    "vibration_sensitivity": 10,
    "reverse_open_close": false,
    "lux_wakeup_enable": true,
    "sensors": {
        "temperature_threshold": 1,
        "temperature_unit": "C"
    },
    "temperature_offset": 0
}

```

### Attributes ###

|           Attribute           | Type |                                                                Description                                                                |
|-------------------------------|------|-------------------------------------------------------------------------------------------------------------------------------------------|
|      `device.sleep_mode`      | bool |                                                               Always `true`                                                               |
|           `actions`           | hash |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-door-window-1-2-settings-actions)|
|       `dark_threshold`        |number|                                                Illumination definition for "dark" in `lux`                                                |
|     `twilight_threshold`      |number|                                              Illumination definition for "twilight" in `lux`                                              |
|      `sleep_mode.period`      |number|                                                      Periodic update period in hours                                                      |
|       `sleep_mode.unit`       |string|                                                                Always `h`                                                                 |
|     `led_status_disable`      | bool |                                                  Whether status LED is enabled/disabled                                                   |
|      `lux_wakeup_enable`      | bool |                                                        Enable wakeup on lux change                                                        |
|        `tilt_enabled`         | bool |                                                   Whether tilt monitoring is activated                                                    |
|       `tilt_calibrated`       | bool |                                                     Whether calibration data is valid                                                     |
|      `vibration_enabled`      | bool |                                                 Whether vibration monitoring is activated                                                 |
|    `vibration_sensitivity`    |number|                                                      Vibration sensitivity, `0..100`                                                      |
|      `lux_wakeup_enable`      | bool |                                            Whether illuminance change can cause device wakeup                                             |
|     `reverse_open_close`      | bool |                                      Whether to reverse which position the sensor consideres "open"                                       |
|`sensors.temperature_threshold`|number|                                 **Door/Window 2 only** Temperature delta (in °C) which triggers an update                                 |
|  `sensors.temperature_unit`   |string|                                                 **Door/Window 2 only** Either `C` or `F`                                                  |
|     `temperature_offset`      |number|                                             **Door/Window 2 only** Temperature offset (in °C)                                             |

Shelly Door/Window accepts the following extra parameters on it's `/settings` endpoint:

### Parameters ###

|       Parameter       | Type |                                            Description                                             |
|-----------------------|------|----------------------------------------------------------------------------------------------------|
|       `actions`       | hash |      For setting actions, see [`/settings/actions`](#shelly-door-window-1-2-settings-actions)      |
|   `dark_threshold`    |number|Illumination definition for "dark" in `lux`, `0..100000` and must be lower than `twilight_threshold`|
| `twilight_threshold`  |number| Illumination definition for "dusk" in `lux`, `0..100000` and must be greater than `dark_threshold` |
| `led_status_disable`  | bool |                                     Enable/disable status LED                                      |
|  `lux_wakeup_enable`  | bool |                                    Enable wakeup on lux change                                     |
| `reverse_open_close`  | bool |                        Reverse which position the sensor consideres "open"                         |
|    `tilt_enabled`     | bool |                                   Enable/disable tilt detection                                    |
|  `vibration_enabled`  | bool |                                 Enable/disable vibration detection                                 |
|`temperature_threshold`|number|             **Door/Window 2 only** Temperature delta (in °C) which triggers an update              |
|  `temperature_units`  |string|                              **Door/Window 2 only** Either `C` or `F`                              |
| `temperature_offset`  |number|                         **Door/Window 2 only** Temperature offset (in °C)                          |
|`vibration_sensitivity`|number|                                Set vibration sensitivity, `0..100`                                 |
|  `lux_wakeup_enable`  | bool |                       Set whether illuminance change can cause device wakeup                       |

Shelly Door/Window 1/2: `/settings/actions`
----------

```
GET /settings/actions (for Door/Window 2)

{
  "actions": {
    "report_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "dark_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "dark_threshold": 100
      }
    ],
    "twilight_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "twilight_threshold": 300
      }
    ],
    "open_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "close_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "vibration_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "temp_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "temp_over_value": 21.5,
        "temp_over_onetime": true
      }
    ],
    "temp_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "temp_under_value": 19.7,
        "temp_under_onetime": false
      }
    ]
  }
}

```

### Actions ###

Shelly Door/Window supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|     Action     |Index|                                               Description                                               |
|----------------|-----|---------------------------------------------------------------------------------------------------------|
|  `report_url`  |  0  |URL to report sensor events on (`/?state=open&lux=100&temp=25.00&tilt=1&vibration=0&id=shellydw2-xxxxxx`)|
|   `dark_url`   |  0  |                            URL to invoke when luminance \<= `dark_threshold`                            |
| `twilight_url` |  0  |         URL to invoke when luminance \> `dark_threshold` AND luminance \<= `twilight_threshold`         |
|   `open_url`   |  0  |                                          URL to invoke on open                                          |
|  `close_url`   |  0  |                                         URL to invoke on close                                          |
|`vibration_url` |  0  |                                  URL to invoke on vibration detection                                   |
|`temp_over_url` |  0  |               **Door/Window 2 only** URL to invoke when temperature \> `temp_over_value`                |
|`temp_under_url`|  0  |               **Door/Window 2 only** URL to invoke when temperature \< `temp_under_value`               |

### Additional parameters ###

|     Parameter      | Type |                                            Description                                             |
|--------------------|------|----------------------------------------------------------------------------------------------------|
|  `dark_threshold`  |number|Illumination definition for "dark" in `lux`, `0..100000` and must be lower than `twilight_threshold`|
|`twilight_threshold`|number| Illumination definition for "dusk" in `lux`, `0..100000` and must be greater than `dark_threshold` |
| `temp_over_value`  |number|              **Door/Window 2 only** Temperature over which to trigger `temp_over_url`              |
|`temp_over_onetime` | bool |    **Door/Window 2 only** Whether the `temp_over_url` will be triggered repeatedly or only once    |
| `temp_under_value` |number|             **Door/Window 2 only** Temperature under which to trigger `temp_under_url`             |
|`temp_under_onetime`| bool |   **Door/Window 2 only** Whether the `temp_under_url` will be triggered repeatedly or only once    |

Shelly Door/Window: `/status`
----------

```
GET /status

{
    "is_valid": true,
    "tmp": {
        "value": 24.3,
        "units": "C",
        "tC": 24.3,
        "tF": 75.74,
        "is_valid": true
    },
    "lux": {
        "value": 0,
        "illumination": "dark",
        "is_valid": true
    },
    "accel": {
        "tilt": 0,
        "vibration": 1,
        "vibration_time": 60,
    },
    "sensor": {
        "state": "close",
        "is_valid": true
    },
    "bat": {
        "value": 71,
        "voltage": 2.73
    },
    "act_reasons": [
        "periodic"
    ]
}

```

### Attributes ###

|      Parameter       |      Type      |                                                           Description                                                            |
|----------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------|
|      `is_valid`      |      bool      |                                            Whether door/window sensor self-checks OK                                             |
|     `tmp.value`      |     number     |                                      **Door/Window 2 only** Temperature in configured units                                      |
|     `tmp.units`      |     string     |                                                **Door/Window 2 only** `C` or `F`                                                 |
|       `tmp.tC`       |     number     |                                             **Door/Window 2 only** Temperature in °C                                             |
|       `tmp.tF`       |     number     |                                             **Door/Window 2 only** Temperature in °F                                             |
|    `tmp.is_valid`    |      bool      |                           **Door/Window 2 only** Whether the temperature sensor is operating properly                            |
|     `lux.value`      |     number     |                                                      Luminance level, `lux`                                                      |
|  `lux.illumination`  |     string     |                   One of `dark`, `twilight` or `bright`; depends on `dark_threshold` and `twilight_threshold`                    |
|    `lux.is_valid`    |      bool      |                                   Whether the internal luminance sensor is operating properly                                    |
|     `accel.tilt`     |     number     |                                                       Tilt in °, `0..180`                                                        |
|  `accel.vibration`   |     number     |                           Whether vibration is detected `0/1`, `-1` if vibration detection is disabled                           |
|`accel.vibration_time`|     number     |                                   If vibration is detected, displays validity time in seconds                                    |
|    `sensor.state`    |     string     |                                           Door/window sensor state: `open` or `close`                                            |
|  `sensor.is_valid`   |      bool      |                                            Whether door/window sensor self-checks OK                                             |
|     `bat.value`      |     number     |                                       Estimated remaining battery capacity in %, `0..100`                                        |
|    `bat.voltage`     |     number     |                                                       Battery voltage, `V`                                                       |
|    `act_reasons`     |array of strings|List of reasons which woke up the device: `battery`, `button`, `periodic`, `poweron`, `sensor`, `movement`, `temperature`, `light`|
|    `sensor_error`    |     number     |                                                 Only displayed in case of error                                                  |

Shelly Door/Window: `/calibrate`
----------

### Parameters ###

|Parameter|Type|                                             Description                                             |
|---------|----|-----------------------------------------------------------------------------------------------------|
| `clear` |bool|                                     `true` = clear calibration                                      |
|`opened` |bool|`true` = request calibration of `opened` position, `false` = request calibration of `closed` position|

Shelly Gas
==========

Shelly Gas: Overview
----------

Shelly Gas is a sensor which can measure combustible gas concentration and issue an alarm in the event of a gas leak.
Shelly Gas operates on AC voltage.

The [product page](https://shelly.cloud/products/shelly-gas-smart-home-automation-sensor/) has all key features described and User Manual.

### LED ###

The center circle-shaped LED indicates the sensor status:

* solid green: sensor is in normal operation
* solid yellow: sensor has a fault
* flashing red: there is an alarm
* flashing red/yellow/green in sequence: sensor is warming up

### Factory Reset ###

To perform a factory reset on a Shelly Gas device:

* hold the user button for 5 seconds to reset WiFi to AP mode
* hold the user button for 10 seconds to perform a complete factory reset

Shelly Gas: MQTT
----------

Shelly Gas **publishes** on the following MQTT topics:

|                     MQTT topic                     |                                Message                                |
|----------------------------------------------------|-----------------------------------------------------------------------|
|  `shellies/shellygas-<deviceid>/sensor/operation`  |                  `unknown` = Sensor state is unknown                  |
|                                                    |                    `warmup` = Sensor is warming up                    |
|                                                    |               `normal` = Sensor is in normal operation                |
|                                                    |                     `fault` = Sensor has a fault                      |
|     `shellies/shellygas-<deviceid>/sensor/gas`     |                  `unknown` = Alarm state is unknown                   |
|                                                    |                      `none` = There is no alarm                       |
|                                                    |                   `mild` = There is a mild gas leak                   |
|                                                    |                  `heavy` = There is a heavy gas leak                  |
|                                                    |             `test` = Issued after a successful self-test              |
|  `shellies/shellygas-<deviceid>/sensor/self_test`  |               `not_completed` = Self-test not completed               |
|                                                    |                   `completed` = Self-test completed                   |
|                                                    |                   `running` = Self-test is running                    |
|                                                    |                `pending` = Self-test scheduled to run                 |
|`shellies/shellygas-<deviceid>/sensor/concentration`|Gas concentration in parts per million: `[0..65535]`, `-1` if not valid|
|   `shellies/shellygas-<deviceid>/valve/0/state`    |                  `unknown` = Valve state is unknown                   |
|                                                    |                      `closed` = Valve is closed                       |
|                                                    |                      `opened` = Valve is opened                       |
|                                                    |               `not_connected` = Valve is not connected                |
|                                                    |                  `failure` = Valve failure detected                   |
|                                                    |            `closing` = Valve is in the process of closing             |
|                                                    |            `opening` = Valve is in the process of opening             |
|                                                    |               `checking` = Valve state is being checked               |

**Note**: by default, Shelly Gas will send periodic MQTT updates every 30 seconds. You can turn these off and only receive messages when there is a change by setting the `mqtt_update_period` parameter to 0 (see [`/settings`](#settings)).

Shelly Gas **subscribes** to the following MQTT topics:

|                      MQTT topic                      |               Message                |
|------------------------------------------------------|--------------------------------------|
|`shellies/shellygas-<deviceid>/sensor/start_self_test`|Any message triggers sensor self-test |
|     `shellies/shellygas-<deviceid>/sensor/mute`      |  Any message mutes an active alarm   |
|    `shellies/shellygas-<deviceid>/sensor/unmute`     | Any message unmutes an active alarm  |
|   `shellies/shellygas-<deviceid>/valve/0/command`    |Accepted values are `close` and `open`|

Shelly Gas: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Gas SHGS-1](docs/coiot/v2/examples/Shelly%20Gas%20SHGS-1)

Shelly Gas: `/settings`
----------

```
GET /settings

{
    "set_volume": 11,
    "actions": {
        "active": false,
        "names": [
            "alarm_off_url",
            "alarm_mild_url",
            "alarm_heavy_url"
        ]
    },
}

```

### Attributes ###

| Attribute  | Type |                                                          Description                                                          |
|------------|------|-------------------------------------------------------------------------------------------------------------------------------|
|`set_volume`|number|                                         Buzzer volume `[1 (lowest) .. 11 (highest)]`                                          |
| `actions`  | hash |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-gas-settings-actions)|

Shelly Gas extends the common [`/settings`](#settings) endpoint with the following parameters:

### Parameters ###

| Parameter  | Type |                                Description                                 |
|------------|------|----------------------------------------------------------------------------|
| `actions`  | hash |For setting actions, see [`/settings/actions`](#shelly-gas-settings-actions)|
|`set_volume`|number|            Set the buzzer volume `[1 (lowest) .. 11 (highest)]`            |

Shelly Gas: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "alarm_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "alarm_mild_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "alarm_heavy_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ]
  }
}

```

### Actions ###

Shelly Gas supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|     Action      |Index|                 Description                 |
|-----------------|-----|---------------------------------------------|
| `alarm_off_url` |  0  |    URL to access when gas alarm is gone     |
|`alarm_mild_url` |  0  |URL to access when there is a mild gas alarm |
|`alarm_heavy_url`|  0  |URL to access when there is a heavy gas alarm|

Shelly Gas: `/settings/valve/0`
----------

If addon manipulator is present, it can be controlled with the following parameters:

### Parameters ###

|Parameter| Type |                Description                 |
|---------|------|--------------------------------------------|
|  `go`   |string|Control the valve, accepts `open` or `close`|

Shelly Gas: `/status`
----------

```
GET /status

{
    "gas_sensor": {
        "sensor_state": "normal",
        "self_test_state": "completed",
        "alarm_state": "none"
    },
    "concentration": {
        "ppm": 100,
        "is_valid": true
    },
    "valves": [
        {
            "state": "not_connected"
        }
    ]
}

```

### Attributes ###

Shelly Gas extends the common [`/status`](#status) endpoint with the following attributes:

|         Attribute          | Type |                                                        Description                                                        |
|----------------------------|------|---------------------------------------------------------------------------------------------------------------------------|
| `gas_sensor.sensor_state`  |string|                                            `unknown` = Sensor state is unknown                                            |
|                            |      |                                              `warmup` = Sensor is warming up                                              |
|                            |      |                                         `normal` = Sensor is in normal operation                                          |
|                            |      |                                               `fault` = Sensor has a fault                                                |
|`gas.sensor.self_test_state`|string|                                         `not_completed` = Self-test not completed                                         |
|                            |      |                                             `completed` = Self-test completed                                             |
|                            |      |                                             `running` = Self-test is running                                              |
|                            |      |                                          `pending` = Self-test scheduled to run                                           |
|  `gas.sensor.alarm_state`  |string|                                            `unknown` = Alarm state is unknown                                             |
|                            |      |                                                `none` = There is no alarm                                                 |
|                            |      |                                             `mild` = There is a mild gas leak                                             |
|                            |      |                                            `heavy` = There is a heavy gas leak                                            |
|                            |      |                                       `test` = Issued after a successful self-test                                        |
|    `concentration.ppm`     |number|                                   Gas concentration in parts per million, `[0..65535]`                                    |
|  `concentration.is_valid`  | bool |                                             `false` = ppm value is not valid                                              |
|                            |      |                                                `true` = ppm value is valid                                                |
|       `valves.state`       |string|State of the addon manipulator: `unknown`, `closed`, `opened`, `not_connected`, `failure`, `closing`, `opening`, `checking`|

Shelly Gas: `/self_test`
----------

```
GET /self_test

{
    "ok": true
}

```

Start sensor self-test

Shelly Gas: `/mute`
----------

```
GET /mute

{
    "ok": true
}

```

Mute active alarm

Shelly Gas: `/unmute`
----------

```
GET /mute

{
    "ok": true
}

```

Unmute active alarm

Shelly Uni
==========

Shelly Uni: Overview
----------

Shelly UNI is the smallest universal module with two available digital inputs and two potential-free outputs, providing endless functionalities.

Shelly Uni has one ADC with two ranges, from 0-12V and 12-30V. It supports up to three temperature sensors and one humidity sensor. Its inputs can operate from 2.2-36V DC and 12-24V AC. The two outputs are up to 36V AC and 24V DC with maximum 100mA current each.
Commands to perform actions can come from:

* A digital input
* HTTP request, trough the local web interface
* A command sent via the cloud
* A weekly-schedule event or a sunrise/sunset-generated event

Shelly Uni supports up to 20 schedule rules.

Product page: <https://shelly.cloud/products/shelly-uni-smart-home-automation-device/>

### Factory Reset ###

If the web interface of the device cannot be accessed, settings can be brought back to default by switching ON and OFF 5 times the physical switch connected to the device, within the first minute after a reboot or power-on.

Each of the two channels is controlled individually and supports the **ON** and **OFF** commands.

Output channels also support `auto_on` and `auto_off` settings -- these are timers in seconds which will turn ON or OFF the channel when it has been turned OFF or ON respectively, from either a physical switch or network command. Thus, the user can set a limit for how long the channel can be **ON** or **OFF**.

Upon power-on, outputs are initialized using one of 4 available strategies:

* Keep output OFF
* Turn output ON
* Restore the state of the output from before the power loss
* Read the physical switch state and configure the output accordingly

Physical input switches can be one of:

* a momentary, push-button switch
* a toggle switch with two stable states
* an "edge" switch. In this input mode, every switch state transition causes a toggle of the output state. This can be used with input from existing two-way switch installations
* detached, inputs do not control the relays
* activation switch

**Note:** Setting output state based on inputs on power-on is not supported when inputs are configured as momentary or edge.

To control Shelly Uni, use these resources:

* [`/settings/relay/{index}`](#shelly-uni-settings-relay-index) to configure the behavior of each channel
* [`/relay/{index}`](#shelly-uni-relay-index) to control and monitor the channel

Shelly Uni: MQTT
----------

Shelly Uni allows control and monitoring over MQTT. Shelly Uni reports:

* `shellies/shellyuni-<deviceid>/input/<i>` for each input `<i>`; reports the current state as `0` or `1`

Input events can be monitored on:

* `shellies/shellyuni-<deviceid>/longpush/<i>` for each input `<i>`; reports a value indicating longpush state as `0` (shortpush) or `1` (longpush)
* `shellies/shellyuni-<deviceid>/input_event/<i>` for each SW input `<i>`; reports input event and event counter, e.g.: `{"event":"S","event_cnt":2}` see [`/status`](#shelly-uni-status) for details

The following topics can be used to read and set output channels `0` and `1`:

* `shellies/shellyuni-<deviceid>/relay/<i>` to report status: `on`, `off` or `overpower`
* `shellies/shellyuni-<deviceid>/relay/<i>/command` accepts `on`, `off` or `toggle`

The following topic can be used to read the adc channel:

* `shellies/shellyuni-<deviceid>/adc/<i>`, which reports the value in volts [V]

Shelly Uni: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly Uni SHUNI-1 no-addon](docs/coiot/v2/examples/Shelly%20Uni%20SHUNI-1)

Shelly Uni: `/settings`
----------

```
GET /settings

{
    "factory_reset_from_switch": true,
    "longpush_time": 1000,
    "actions": {
        "active": false,
        "names": [
            "out_off_url",
            "out_on_url",
            "btn_on_url",
            "btn_off_url",
            "longpush_url",
            "shortpush_url",
            "out_on_url",
            "out_off_url",
            "btn_on_url",
            "btn_off_url",
            "longpush_url",
            "shortpush_url",
            "adc_over_url",
            "adc_under_url",
            "ext_temp_over_url",
            "ext_temp_under_url",
            "ext_hum_over_url",
            "ext_hum_under_url"
        ]
    },
    "relays": [
      {
        "name": null,
        "ison": false,
        "has_timer": false,
        "default_state": "off",
        "btn_type": "toggle",
        "btn_reverse": 0,
        "auto_on": 0,
        "auto_off": 0,
        "schedule": false,
        "schedule_rules": []
      },
      {
        "name": null,
        "ison": false,
        "has_timer": false,
        "default_state": "off",
        "btn_type": "toggle",
        "btn_reverse": 0,
        "auto_on": 0,
        "auto_off": 0,
        "schedule": false,
        "schedule_rules": []
      }
    ],
    "adcs": [
      {
        "range": 30,
        "relay_actions": [
          {
            "over_threshold": 0,
            "over_act": "disabled",
            "under_threshold": 0,
            "under_act": "disabled"
          },
          {
            "over_threshold": 0,
            "over_act": "disabled",
            "under_threshold": 0,
            "under_act": "disabled"
          }
        ]
      }
    ],
    "ext_sensors": {
      "temperature_unit": "C"
    },
    "ext_temperature": {
      "0": [
        {
          "overtemp_threshold_tC": 0,
          "overtemp_threshold_tF": 32,
          "undertemp_threshold_tC": 0,
          "undertemp_threshold_tF": 32,
          "overtemp_act": "disabled",
          "undertemp_act": "disabled",
          "offset_tC": 0,
          "offset_tF": 0
        },
        {
          "overtemp_threshold_tC": 0,
          "overtemp_threshold_tF": 32,
          "undertemp_threshold_tC": 0,
          "undertemp_threshold_tF": 32,
          "overtemp_act": "disabled",
          "undertemp_act": "disabled",
          "offset_tC": 0,
          "offset_tF": 0
        }
      ],
  },
  "ext_humidity": {}
}

```

Shelly Uni extends the common `/settings` endpoint with relay and adc specific data and contains the settings for this device and adds [`/settings/relay/{index}`](#shelly-uni-settings-relay-index) parameters.

### Attributes ###

|         Attribute         |     Type      |                                                          Description                                                          |
|---------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------|
|`factory_reset_from_switch`|     bool      |                              Whether factory reset via 5-time flip of an input switch is enabled                              |
|          `mode`           |    string     |                                                        Always `relay`                                                         |
|      `longpush_time`      |    number     |                                              Duration to detect long push, `ms`                                               |
|         `actions`         |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-uni-settings-actions)|
|         `relays`          |array of hashes|                  See [`/settings/relay/{index}`](#shelly-uni-settings-relay-index) for explanation of values                  |
|          `adcs`           |     hash      |                         See [`/settings/adc/0`](#shelly-uni-settings-adc-0) for explanation of values                         |

### Parameters ###

|         Parameter         | Type |                                   Description                                   |
|---------------------------|------|---------------------------------------------------------------------------------|
|`factory_reset_from_switch`| bool |         Enable/disable factory reset via 5-time flip of an input switch         |
|         `actions`         | hash |  For setting actions, see [`/settings/actions`](#shelly-uni-settings-actions)   |
|          `adcs`           | hash |See [`/settings/adc/0`](#shelly-uni-settings-adc-0) for explanation of parameters|
|      `longpush_time`      |number|                  Set duration to detect long push, `1..5000ms`                  |

Shelly Uni: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "btn_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "btn_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "longpush_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "shortpush_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_on_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false
      }
    ],
    "adc_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "adc_over_value": 1200,
        "adc_over_onetime": false
      }
    ],
    "adc_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "adc_under_value": 1000,
        "adc_under_onetime": false
      }
    ],
    "ext_temp_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_temp_over_value": 24.0,
        "ext_temp_over_onetime": false
      }
    ],
    "ext_temp_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_temp_under_value": 22.5,
        "ext_temp_under_onetime": false
      }
    ],
    "ext_hum_over_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_hum_over_value": 60,
        "ext_hum_over_onetime": false
      }
    ],
    "ext_hum_under_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "ext_hum_under_value": 40,
        "ext_hum_under_onetime": false
      }
    ]
  }
}

```

### Actions ###

Shelly Uni supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

|       Action       |Index|                                                     Description                                                      |
|--------------------|-----|----------------------------------------------------------------------------------------------------------------------|
|    `btn_on_url`    | 0-1 |                                       URL to access when SW input is activated                                       |
|   `btn_off_url`    | 0-1 |                                      URL to access when SW input is deactivated                                      |
|    `out_on_url`    | 0-1 |                                        URL to access when output is activated                                        |
|   `out_off_url`    | 0-1 |                                       URL to access when output is deactivated                                       |
|   `longpush_url`   | 0-1 |URL to access on longpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`. |
|  `shortpush_url`   | 0-1 |URL to access on shortpush. Works only when button is configured as `momentary`, `momentary_on_release` or `detached`.|
|   `adc_over_url`   |  0  |                                   URL to invoke when adc value \> `adc_over_value`                                   |
|  `adc_under_url`   |  0  |                                  URL to invoke when adc value \< `adc_under_value`                                   |
|`ext_temp_over_url` | 0-2 |              **If temperature sensor attached** URL to invoke when temperature \> `ext_temp_over_value`              |
|`ext_temp_under_url`| 0-2 |             **If temperature sensor attached** URL to invoke when temperature \< `ext_temp_under_value`              |
| `ext_hum_over_url` |  0  |           **If humidity sensor attached (DHT22 only)** URL to invoke when humidity \> `ext_hum_over_value`           |
|`ext_hum_under_url` |  0  |          **If humidity sensor attached (DHT22 only)** URL to invoke when humidity \< `ext_hum_under_value`           |

### Additional parameters ###

|       Parameter        | Type |                               Description                                |
|------------------------|------|--------------------------------------------------------------------------|
|    `adc_over_value`    |number|          ADC value, in mV, over which to trigger `adc_over_url`          |
|   `adc_over_onetime`   | bool |   Whether the `adc_over_url` will be triggered repeatedly or only once   |
|   `adc_under_value`    |number|         ADC value, in mV, under which to trigger `adc_under_url`         |
|  `adc_under_onetime`   | bool |  Whether the `adc_under_url` will be triggered repeatedly or only once   |
| `ext_temp_over_value`  |number|          Temperature over which to trigger `ext_temp_over_url`           |
|`ext_temp_over_onetime` | bool |Whether the `ext_temp_over_url` will be triggered repeatedly or only once |
| `ext_temp_under_value` |number|         Temperature under which to trigger `ext_temp_under_url`          |
|`ext_temp_under_onetime`| bool |Whether the `ext_temp_under_url` will be triggered repeatedly or only once|
|  `ext_hum_over_value`  |number|            Humidity over which to trigger `ext_hum_over_url`             |
| `ext_hum_over_onetime` | bool | Whether the `ext_hum_over_url` will be triggered repeatedly or only once |
| `ext_hum_under_value`  |number|           Humidity under which to trigger `ext_hum_under_url`            |
|`ext_hum_under_onetime` | bool |Whether the `ext_hum_under_url` will be triggered repeatedly or only once |

Shelly Uni: `/settings/relay/{index}`
----------

```
GET /settings/relay/0

{
    "name": null,
    "appliance_type": "General",
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "btn_type": "toggle",
    "btn_reverse": 0,
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": []
}

```

The returned document here is identical to the data returned in `/settings` for the particular output channel in the `relays` array. The attributes match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                                              Description                                               |
|----------------|----------------|--------------------------------------------------------------------------------------------------------|
|     `name`     |     string     |                                               Relay name                                               |
|`appliance_type`|     string     |                                   Custom configurable appliance type                                   |
|     `ison`     |      bool      |                                             Channel state                                              |
|  `has_timer`   |      bool      |                            Whether there is an active timer on the channel                             |
|  `overpower`   |      bool      |                              Whether an overpower condition has occurred                               |
|`default_state` |     string     |                      Default power-on state, one of `off`, `on`, `last`, `switch`                      |
|   `btn_type`   |     string     |Button type, one of `momentary`, `toggle`, `edge`, `detached`, `action`, `cycle`, `momentary_on_release`|
| `btn_reverse`  |     number     |                                 Whether input switch state is inverted                                 |
|   `auto_on`    |     number     |             Automatic flip back timer, seconds. Will engage after turning the channel OFF              |
|   `auto_off`   |     number     |              Automatic flip back timer, seconds. Will engage after turning the channel ON              |
|   `schedule`   |      bool      |                                     Whether scheduling is enabled                                      |
|`schedule_rules`|array of strings|                                     Rules for schedule activation                                      |

### Parameters ###

|   Parameter    |      Type      |                                           Description                                            |
|----------------|----------------|--------------------------------------------------------------------------------------------------|
|    `reset`     |      any       |Submitting a non-empty value will reset settings for this relay output channel to factory defaults|
|     `name`     |     string     |                                            Relay name                                            |
|`appliance_type`|     string     |                              Set custom configurable appliance type                              |
|`default_state` |     string     |                          Accepted values: `off`, `on`, `last`, `switch`                          |
|   `btn_type`   |     string     |   Accepted values: `momentary`, `toggle`, `edge`, `detached`, `action`, `momentary_on_release`   |
| `btn_reverse`  |      bool      |                              Inverts the logical state of the input                              |
|   `auto_on`    |     number     |          Automatic flip back timer, seconds. Will engage after turning the channel OFF           |
|   `auto_off`   |     number     |           Automatic flip back timer, seconds. Will engage after turning the channel ON           |
|   `schedule`   |      bool      |                                      Enable schedule timer                                       |
|`schedule_rules`|array of strings|                      Rules for schedule activation, e.g. `0000-0123456-on`                       |

Shelly Uni: `/settings/adc/0`
----------

```
GET /settings/adc/0

{
  "range": 30,
  "relay_actions": [
    {
      "over_threshold": 0,
      "over_act": "disabled",
      "under_threshold": 0,
      "under_act": "disabled"
    },
    {
      "over_threshold": 0,
      "over_act": "disabled",
      "under_threshold": 0,
      "under_act": "disabled"
    }
  ]
}

```

### Attributes ###

|   Attribute   |     Type      |                Description                 |
|---------------|---------------|--------------------------------------------|
|    `range`    |    number     |12 or 30, Range of the adc (0-12V or 12-30V)|
|`relay_actions`|array of hashes|           ADC automation actions           |

### `relay_actions.{index}` attributes ###

|    Attribute    |     Type      |                          Description                          |
|-----------------|---------------|---------------------------------------------------------------|
|`over_threshold` |    number     |                   Overvoltage threshold, mV                   |
|   `over_act`    |    string     |Overvoltage action, one of `disabled`, `relay_on`, `relay_off` |
|`under_threshold`|    number     |                  Undervoltage threshold, mV                   |
|   `under_act`   |array of hashes|Undervoltage action, one of `disabled`, `relay_on`, `relay_off`|

### Parameters ###

|   Parameter   |     Type      |                Description                 |
|---------------|---------------|--------------------------------------------|
|    `range`    |    number     |12 or 30, Range of the adc (0-12V or 12-30V)|
|`relay_actions`|array of hashes|           ADC automation actions           |

### `relay_actions.{index}` parameters ###

|    Parameter    |     Type      |                          Description                          |
|-----------------|---------------|---------------------------------------------------------------|
|`over_threshold` |    number     |                   Overvoltage threshold, mV                   |
|   `over_act`    |    string     |Overvoltage action, one of `disabled`, `relay_on`, `relay_off` |
|`under_threshold`|    number     |                  Undervoltage threshold, mV                   |
|   `under_act`   |array of hashes|Undervoltage action, one of `disabled`, `relay_on`, `relay_off`|

Shelly Uni: `/status`
----------

```
GET /status

"relays": [
    {
        "ison": false,
        "has_timer": false,
        "timer_started": 0,
        "timer_duration": 0,
        "timer_remaining": 0,
        "overpower": false,
        "is_valid": true,
        "source": "http"
    },
    {
        "ison": false,
        "has_timer": false,
        "timer_started": 0,
        "timer_duration": 0,
        "timer_remaining": 0,
        "overpower": false,
        "is_valid": true,
        "source": "cloud"
    }
],
"inputs": [
  {
      "input": 0,
      "event": "S",
      "event_cnt": 2
  },
  {
      "input": 0,
      "event": "S",
      "event_cnt": 2
  }
],
"adcs": [
  {
    "voltage": 11.31
  }
],
"ext_sensors": {
  "temperature_unit": "C"
},
"ext_temperature": {
  "0": {
    "hwID": "287169120c0000d7",
    "tC": 24.5,
    "tF": 76.1
  }
},
"ext_humidity": {}
]

```

### Attributes ###

|Attribute|     Type      |                                                                            Description                                                                            |
|---------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`relays` |array of hashes|Displayed in **Relay** mode: Contains the current state of the relay output channels. See [`/relay/{index}`](#shelly-uni-relay-index) for description of attributes|
|`inputs` |array of hashes|                                                        Current state of the inputs, see description below                                                         |
| `adcs`  |array of hashes|                                                          Current state of the adc, see description below                                                          |

### `inputs.{index}` attributes ###

| Attribute | Type |                          Description                           |
|-----------|------|----------------------------------------------------------------|
|  `input`  |number|                   Current state of the input                   |
|  `event`  |string|Last input event, `S`=shortpush, `L`=longpush, `""`=none/invalid|
|`event_cnt`|number|                    Event counter, `uint16`                     |

`input` shows the current logical state of the input: `0`=OFF and `1`=ON.`event` provides a short string, designating the last detected input event (shortpush/longpush).`event_cnt` is incremented each time a new input event occurs. `event_cnt` is not stored in non-volatile memory.

Input events have a lifetime of 5s; after this `event` will be cleared to `""`.

Input events are only detected when `btn_type` is configured as `momentary`, `momentary_on_release` or `detached`.

### `adcs.{index}` attributes ###

|Attribute| Type |     Description      |
|---------|------|----------------------|
|`voltage`|number|Value of the adc, in V|

Shelly Uni: `/relay/{index}`
----------

```
GET /relay/0

{
    "ison": true,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "is_valid": false,
    "source": "http"
}

```

Shows current status of each output channel and accepts commands for controlling the channel. This is usable only when device mode is set to `relay` via [`/settings`](#shelly-uni-settings).

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                    Whether an overpower condition turned the channel OFF                     |
|   `is_valid`    | bool |                 Whether the associated power meter is functioning correctly                  |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                                    Description                                                    |
|---------|------|-------------------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`, `toggle`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                       A one-shot flip-back timer in seconds                                       |

Shelly EM
==========

Shelly EM: Overview
----------

Shelly EM measures electrical consumption on two channels (shared phase) and allows for controlling one low-power external appliance.

Shelly EM supports up to 20 schedule rules.

[Product page](https://shelly.cloud/products/shelly-em-smart-home-automation-device/)

### Factory Reset ###

To perform a factory reset, if doing so from the web interface or application is not possible -- press and hold the built-in user button until the LED starts blinking rapidly.

Shelly EM: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly EM reports data on:

* `shellies/shellyem-<deviceid>/emeter/<i>/energy` energy counter in Watt-minute
* `shellies/shellyem-<deviceid>/emeter/<i>/returned_energy` energy returned to the grid in Watt-minute
* `shellies/shellyem-<deviceid>/emeter/<i>/total` total energy in `Wh` (accumulated in device's non-volatile memory)
* `shellies/shellyem-<deviceid>/emeter/<i>/total_returned` total energy returned to the grid in `Wh` (accumulated in device's non-volatile memory)
* `shellies/shellyem-<deviceid>/emeter/<i>/power` instantaneous active power in Watts
* `shellies/shellyem-<deviceid>/emeter/<i>/reactive_power` instantaneous reactive power in Watts
* `shellies/shellyem-<deviceid>/emeter/<i>/voltage` grid voltage in Volts
* `shellies/shellyem-<deviceid>/relay/0` reports status: `on`, `off` or `overpower`

Note, that `energy` and `returned_energy` do not survive power cycle or reboot -- this is how the value is implemented on other Shellies. Shelly EM features a persisted version which is not affected by power cycling or lack of connectivity. To get the persisted counters use `total` and `total_returned`.

Commands are accepted on:

* `shellies/shellyem-<deviceid>/relay/0/command` accepts `on`, `off` or `toggle`
* `shellies/shellyem-<deviceid>/emeter/<i>/command` accepts message `reset_totals` to reset `total` and `total_returned` energy counters to 0
* `shellies/shellyem-<deviceid>/command` accepts message `reset_data` to reset all device data

Shelly EM: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly EM SHEM](docs/coiot/v2/examples/Shelly%20EM%20SHEM)

Shelly EM: `/settings`
----------

```
GET /settings

{
    "actions": {
        "active": false,
        "names": [
            "out_on_url",
            "out_off_url",
            "over_power_url",
            "under_power_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "off",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        }
    ],
    "emeters": [
        {
            "appliance_type": "General",
            "ctraf_type": 50,
            "max_power": 0
        },
        {
            "appliance_type": "General",
            "ctraf_type": 50,
            "max_power": 0
        }
    ],
    "led_status_disable": false
}

```

### Attributes ###

|     Attribute      |     Type      |                                                         Description                                                          |
|--------------------|---------------|------------------------------------------------------------------------------------------------------------------------------|
|`led_status_disable`|     bool      |                                           Whether LED status indication is enabled                                           |
|     `actions`      |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-em-settings-actions)|
|      `relays`      |array of hashes|                            Relay settings, see [`/settings/relay/0`](#shelly-em-settings-relay-0)                            |
|     `emeters`      |array of hashes|                EM channels configuration, see [`/settings/emeter/{index}`](#shelly-em-settings-emeter-index)                 |

[Common parameters](#settings) apply for the `/settings` endpoint. Additionally:

### Parameters ###

|     Parameter      | Type |                                                                           Description                                                                            |
|--------------------|------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`led_status_disable`| bool |                                                                  Disable LED status indication                                                                   |
|     `actions`      | hash |                                           For setting actions, see [`/settings/actions`](#shelly-em-settings-actions)                                            |
|     `set_time`     |string|Time and date manual setting in format `[yyyy][mm][dd][hh][mm][ss][utc_offset_sec]`, for example `settings/?set_time=20200328151600-120` means 2020-03-28 15:16:00|

Shelly EM: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "over_power_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      }
    ],
    "under_power_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      }
    ]
  }
}

```

Shelly EM supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

### Actions ###

|     Action      |Index|                       Description                       |
|-----------------|-----|---------------------------------------------------------|
|  out\_on\_url   |  0  |         URL to access when output is activated          |
|  out\_off\_url  |  0  |        URL to access when output is deactivated         |
|over\_power\_url |  0  |URL to invoke when `over_power_url_threshold` is reached |
|under\_power\_url|  0  |URL to invoke when `under_power_url_threshold` is reached|

### Additional parameters ###

|         Parameter         | Type |                       Description                        |
|---------------------------|------|----------------------------------------------------------|
|`over_power_url_threshold` |number|Threshold in `W` to trigger over\_power\_url when crossed |
|`under_power_url_threshold`|number|Threshold in `W` to trigger under\_power\_url when crossed|

Shelly EM: `/settings/relay/0`
----------

```
GET /settings/relay/0

{
    "name": null,
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": []
}

```

This is identical to `/settings/relay/{index}` endpoints on most other Shelly devices with built in relays. The returned document is identical to the data returned in `/settings` for the single output channel in the `relays` array. The channel index exists to preserve API compatibility with multi-channel Shelly devices. Attributes in the response match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                      Description                      |
|----------------|----------------|-------------------------------------------------------|
|     `name`     |     string     |                      Relay name                       |
|     `ison`     |      bool      |                      Relay state                      |
|  `has_timer`   |      bool      |           Whether there is an active timer            |
|  `overpower`   |      bool      |      Whether an overpower condition has occurred      |
|`default_state` |     string     |State on power-on, one of `off`, `on`, `last`, `switch`|
|   `auto_on`    |     number     |          Automatic flip back timer, seconds           |
|   `auto_off`   |     number     |          Automatic flip back timer, seconds           |
|   `schedule`   |      bool      |             Whether scheduling is enabled             |
|`schedule_rules`|array of strings|             Rules for schedule activation             |

### Parameters ###

|   Parameter    |      Type      |                                    Description                                    |
|----------------|----------------|-----------------------------------------------------------------------------------|
|    `reset`     |      any       |Submitting a non-empty value will reset settings for the output to factory defaults|
|     `name`     |     string     |                                  Set relay name                                   |
|`default_state` |     string     |                  Accepted values: `off`, `on`, `last`, `switch`                   |
|   `auto_on`    |     number     |         Automatic flip back timer, seconds. Will engage after turning OFF         |
|   `auto_off`   |     number     |         Automatic flip back timer, seconds. Will engage after turning ON          |
|   `schedule`   |      bool      |                               Enable schedule timer                               |
|`schedule_rules`|array of strings|               Rules for schedule activation, e.g. `0000-0123456-on`               |

Shelly EM: `/settings/emeter/{index}`
----------

```
GET /settings/emeter/0

{
    "appliance_type": "General",
    "ctraf_type": 50,
    "max_power": 0
}

```

This endpoint allows for configuring over/under-power actions and max power protection.

### Attributes ###

|   Attribute    | Type |                        Description                        |
|----------------|------|-----------------------------------------------------------|
|`appliance_type`|string|            Custom configurable appliance type             |
|  `ctraf_type`  |number|Current transformer type, `50` or `120` - currently unused |
|  `max_power`   |number|Maximum allowed power before contactor is switched off, `W`|

### Parameters ###

|   Parameter    | Type |                          Description                          |
|----------------|------|---------------------------------------------------------------|
|`appliance_type`|string|            Set custom configurable appliance type             |
|  `ctraf_type`  |number|Set current transformer type, `50` or `120` - currently unused |
|  `max_power`   |number|Set maximum allowed power before contactor is switched off, `W`|

Shelly EM: `/status`
----------

```
GET /status

{
    "relays": [
        {
            "ison": false,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "is_valid": true,
            "source": "http"
        }
    ],
    "emeters": [
        {
            "power": 0,
            "reactive": 0,
            "voltage": 0,
            "is_valid": true,
            "total": 0,
            "total_returned": 0
        },
        {
            "power": 0,
            "reactive": 0,
            "voltage": 0,
            "is_valid": true,
            "total": 0,
            "total_returned": 0
        }
    ]
}

```

In addition to common status info, EM adds:

### Attributes ###

|Attribute|     Type      |                              Description                               |
|---------|---------------|------------------------------------------------------------------------|
|`relays` |array of hashes|   Status of the internal relay, see [`/relay/0`](#shelly-em-relay-0)   |
|`emeters`|array of hashes|Current meter readings, see [`/emeter/{index}`](#shelly-em-emeter-index)|

Shelly EM: `/relay/0`
----------

```
GET /relay/0

{
    "ison": false,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "is_valid": true,
    "source": "http"
}

```

Returns the state of the internal relay.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                         Whether an overpower condition has occurred                          |
|   `is_valid`    | bool |                                Whether power result is valid                                 |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                               Description                                               |
|---------|------|---------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                  A one-shot flip-back timer in seconds                                  |

Shelly EM: `/emeter/{index}`
----------

```
GET /emeter/0

{
    "power": 0,
    "reactive": 0,
    "voltage": 0,
    "is_valid": true,
    "total": 0,
    "total_returned": 0
}

```

### Attributes ###

|   Attribute    | Type |                    Description                     |
|----------------|------|----------------------------------------------------|
|    `power`     |number|            Instantaneous power, `Watts`            |
|   `reactive`   |number|       Instantaneous reactive power, `Watts`        |
|   `voltage`    |number|                RMS voltage, `Volts`                |
|   `is_valid`   | bool |Whether the associated meter is functioning properly|
|    `total`     |number|            Total consumed energy, `Wh`             |
|`total_returned`|number|            Total returned energy, `Wh`             |

### Parameters ###

|  Parameter   |Type|                                Description                                |
|--------------|----|---------------------------------------------------------------------------|
|`reset_totals`|any |When requested will reset `total` and `total_returned` energy counters to 0|

Shelly EM: `/emeter/{index}/em_data.csv`
----------

This provides an export of the data gathered by the device. For each measurement channel, a CSV file is generated with the following columns:

* Date/time UTC
* Active energy Wh
* Returned energy Wh
* Min V
* Max V

This will always contain data for the entire time range stored on the device.

Shelly EM: `/reset_data`
----------

```
GET /reset_data

{
    "reset_data": 1
}

```

When requested will reset all device data.

Shelly 3EM
==========

Shelly 3EM: Overview
----------

Shelly 3EM is a professional 3-phase energy meter with the following features:

* Precise 3-phase energy metering
* Up to 120A per phase
* Integrated 10A contactor control
* Solar and Wind power compatible
* Factory calibrated with over 99% accuracy
* DIN mountable
* Wi-Fi enabled
* Cloud and MQTT Enabled
* 365 days power consumption history
* Anti energy theft protection

Shelly 3EM supports up to 20 schedule rules.

[Product page](https://shelly.cloud/products/shelly-3em-smart-home-automation-energy-meter/)

### Factory Reset ###

To perform a factory reset, if doing so from the web interface or application is not possible -- press and hold the built-in user button until the LED starts blinking rapidly.

Shelly 3EM: MQTT
----------

When configured for [MQTT](#mqtt-support) Shelly 3EM reports data on:

* `shellies/shellyem3-<deviceid>/emeter/<i>/energy` energy counter in Watt-minute since last report
* `shellies/shellyem3-<deviceid>/emeter/<i>/returned_energy` energy returned to the grid in Watt-minute since last report
* `shellies/shellyem3-<deviceid>/emeter/<i>/total` total energy in `Wh` (accumulated in device's non-volatile memory)
* `shellies/shellyem3-<deviceid>/emeter/<i>/total_returned` total energy returned to the grid in `Wh` (accumulated in device's non-volatile memory)
* `shellies/shellyem3-<deviceid>/emeter/<i>/power` instantaneous active power in Watts
* `shellies/shellyem3-<deviceid>/emeter/<i>/voltage` grid voltage in Volts
* `shellies/shellyem3-<deviceid>/emeter/<i>/current` current in Amps
* `shellies/shellyem3-<deviceid>/emeter/<i>/pf` power factor (dimensionless)
* `shellies/shellyem3-<deviceid>/relay/0` reports status: `on`, `off` or `overpower`

Note, that `energy` and `returned_energy` do not survive power cycle or reboot -- this is how the value is implemented on other Shellies. Shelly 3EM features a persisted version which is not affected by power cycling or lack of connectivity. To get the persisted counters use `total` and `total_returned`.

Commands are accepted on:

* `shellies/shellyem3-<deviceid>/relay/0/command` accepts `on`, `off` or `toggle`
* `shellies/shellyem3-<deviceid>/emeter/<i>/command` accepts message `reset_totals` to reset `total` and `total_returned` energy counters to 0
* `shellies/shellyem3-<deviceid>/command` accepts message `reset_data` to reset all device data

Shelly 3EM: CoIoT
----------

Example CoIoT description (`/cit/d`) and status (`/cit/s`):

* [Shelly 3EM SHEM-3](docs/coiot/v2/examples/Shelly%203EM%20SHEM-3)

Shelly 3EM: `/settings`
----------

```
GET /settings

{
    "actions": {
        "active": false,
        "names": [
            "out_on_url",
            "out_off_url",
            "over_power_url",
            "under_power_url"
        ]
    },
    "relays": [
        {
            "name": null,
            "ison": false,
            "has_timer": false,
            "overpower": false,
            "default_state": "off",
            "auto_on": 0,
            "auto_off": 0,
            "schedule": false,
            "schedule_rules": []
        }
    ],
    "emeters": [
        {
            "appliance_type": "General",
            "max_power": 0
        },
        {
            "appliance_type": "General",
            "max_power": 0
        },
        {
            "appliance_type": "General",
            "max_power": 0
        }
    ],
    "led_status_disable": false
}

```

### Attributes ###

|     Attribute      |     Type      |                                                          Description                                                          |
|--------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------|
|`led_status_disable`|     bool      |                                           Whether LED status indication is enabled                                            |
|     `actions`      |     hash      |List with all supported url actions. For detailed actions descriptions, see [`/settings/actions`](#shelly-3em-settings-actions)|
|      `relays`      |array of hashes|                            Relay settings, see [`/settings/relay/0`](#shelly-3em-settings-relay-0)                            |
|     `emeters`      |array of hashes|                3EM channels configuration, see [`/settings/emeter/{index}`](#shelly-3em-settings-emeter-index)                |

[Common parameters](#settings) apply for the `/settings` endpoint. Additionally:

### Parameters ###

|     Parameter      | Type |                                                                           Description                                                                            |
|--------------------|------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`led_status_disable`| bool |                                                                  Disable LED status indication                                                                   |
|     `actions`      | hash |                                           For setting actions, see [`/settings/actions`](#shelly-3em-settings-actions)                                           |
|     `set_time`     |string|Time and date manual setting in format `[yyyy][mm][dd][hh][mm][ss][utc_offset_sec]`, for example `settings/?set_time=20200328151600-120` means 2020-03-28 15:16:00|

Shelly 3EM: `/settings/actions`
----------

```
GET /settings/actions

{
  "actions": {
    "out_on_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "out_off_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false
      }
    ],
    "over_power_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      }
    ],
    "under_power_url": [
      {
        "index": 0,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      }
    ],
    "over_power_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      }
    ],
    "under_power_url": [
      {
        "index": 1,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      }
    ],
    "over_power_url": [
      {
        "index": 2,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      }
    ],
    "under_power_url": [
      {
        "index": 2,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      }
    ],
    "over_power_url": [
      {
        "index": 3,
        "urls": [],
        "enabled": false,
        "over_power_url_threshold": 0
      }
    ],
    "under_power_url": [
      {
        "index": 3,
        "urls": [],
        "enabled": false,
        "under_power_url_threshold": 0
      }
    ]
  }
}

```

Shelly 3EM supports the following actions, which can be set as described at [`/settings/actions`](https://shelly-api-docs.shelly.cloud/#settings-actions):

### Actions ###

|     Action      |Index|                                                  Description                                                   |
|-----------------|-----|----------------------------------------------------------------------------------------------------------------|
|  out\_on\_url   |  0  |                                     URL to access when output is activated                                     |
|  out\_off\_url  |  0  |                                    URL to access when output is deactivated                                    |
|over\_power\_url |  0  |                            URL to invoke when `over_power_url_threshold` is reached                            |
|under\_power\_url|  0  |                           URL to invoke when `under_power_url_threshold` is reached                            |
|over\_power\_url |  1  |                            URL to invoke when `over_power_url_threshold` is reached                            |
|under\_power\_url|  1  |                           URL to invoke when `under_power_url_threshold` is reached                            |
|over\_power\_url |  2  |                            URL to invoke when `over_power_url_threshold` is reached                            |
|under\_power\_url|  2  |                           URL to invoke when `under_power_url_threshold` is reached                            |
|over\_power\_url |  3  |URL to invoke when `over_power_url_threshold` is reached. Index 3 is applied for the sum of the three channels. |
|under\_power\_url|  3  |URL to invoke when `under_power_url_threshold` is reached. Index 3 is applied for the sum of the three channels.|

### Additional parameters ###

|         Parameter         | Type |                       Description                        |
|---------------------------|------|----------------------------------------------------------|
|`over_power_url_threshold` |number|Threshold in `W` to trigger over\_power\_url when crossed |
|`under_power_url_threshold`|number|Threshold in `W` to trigger under\_power\_url when crossed|

Shelly 3EM: `/settings/relay/0`
----------

```
GET /settings/relay/0

{
    "name": null,
    "ison": false,
    "has_timer": false,
    "overpower": false,
    "default_state": "off",
    "auto_on": 0,
    "auto_off": 0,
    "schedule": false,
    "schedule_rules": []
}

```

This is identical to `/settings/relay/{index}` endpoints on most other Shelly devices with built in relays. The returned document is identical to the data returned in `/settings` for the single output channel in the `relays` array. The channel index exists to preserve API compatibility with multi-channel Shelly devices. Attributes in the response match the set of accepted parameters.

### Attributes ###

|   Attribute    |      Type      |                      Description                      |
|----------------|----------------|-------------------------------------------------------|
|     `name`     |     string     |                      Relay name                       |
|     `ison`     |      bool      |                      Relay state                      |
|  `has_timer`   |      bool      |           Whether there is an active timer            |
|  `overpower`   |      bool      |      Whether an overpower condition has occurred      |
|`default_state` |     string     |State on power-on, one of `off`, `on`, `last`, `switch`|
|   `auto_on`    |     number     |          Automatic flip back timer, seconds           |
|   `auto_off`   |     number     |          Automatic flip back timer, seconds           |
|   `schedule`   |      bool      |             Whether scheduling is enabled             |
|`schedule_rules`|array of strings|             Rules for schedule activation             |

### Parameters ###

|   Parameter    |      Type      |                                    Description                                    |
|----------------|----------------|-----------------------------------------------------------------------------------|
|    `reset`     |      any       |Submitting a non-empty value will reset settings for the output to factory defaults|
|     `name`     |     string     |                                  Set relay name                                   |
|`default_state` |     string     |                  Accepted values: `off`, `on`, `last`, `switch`                   |
|   `auto_on`    |     number     |         Automatic flip back timer, seconds. Will engage after turning OFF         |
|   `auto_off`   |     number     |         Automatic flip back timer, seconds. Will engage after turning ON          |
|   `schedule`   |      bool      |                               Enable schedule timer                               |
|`schedule_rules`|array of strings|               Rules for schedule activation, e.g. `0000-0123456-on`               |

Shelly 3EM: `/settings/emeter/{index}`
----------

```
GET /settings/emeter/0

{
    "appliance_type": "General",
    "max_power": 0
}

```

This endpoint allows for configuring over/under-power actions and max power protection.

### Attributes ###

|   Attribute    | Type |                        Description                        |
|----------------|------|-----------------------------------------------------------|
|`appliance_type`|string|            Custom configurable appliance type             |
|  `max_power`   |number|Maximum allowed power before contactor is switched off, `W`|

### Parameters ###

|   Parameter    | Type |                          Description                          |
|----------------|------|---------------------------------------------------------------|
|`appliance_type`|string|            Set custom configurable appliance type             |
|  `max_power`   |number|Set maximum allowed power before contactor is switched off, `W`|

Shelly 3EM: `/status`
----------

```
GET /status

{
    "relays": [
        {
            "ison": false,
            "has_timer": false,
            "timer_started": 0,
            "timer_duration": 0,
            "timer_remaining": 0,
            "overpower": false,
            "is_valid": true,
            "source": "http"
        }
    ],
    "emeters": [
        {
            "power": 0,
            "pf": 0,
            "current": 0,
            "voltage": 0,
            "is_valid": true,
            "total": 0,
            "total_returned": 0
        },
        {
            "power": 0,
            "pf": 0,
            "current": 0,
            "voltage": 0,
            "is_valid": true,
            "total": 0,
            "total_returned": 0
        },
        {
            "power": 0,
            "pf": 0,
            "current": 0,
            "voltage": 0,
            "is_valid": true,
            "total": 0,
            "total_returned": 0
        }
    ],
    "total_power": 67.50,
    "fs_mounted": true
}

```

In addition to common status info, 3EM adds:

### Attributes ###

|  Attribute  |     Type      |                               Description                               |
|-------------|---------------|-------------------------------------------------------------------------|
|  `relays`   |array of hashes|   Status of the internal relay, see [`/relay/0`](#shelly-3em-relay-0)   |
|  `emeters`  |array of hashes|Current meter readings, see [`/emeter/{index}`](#shelly-3em-emeter-index)|
|`total_power`|    number     |             Sum of the power of the three channels, `Watts`             |
|`fs_mounted` |     bool      |                       Whether sysflash is mounted                       |

Shelly 3EM: `/relay/0`
----------

```
GET /relay/0

{
    "ison": false,
    "has_timer": false,
    "timer_started": 0,
    "timer_duration": 0,
    "timer_remaining": 0,
    "overpower": false,
    "is_valid": true,
    "source": "http"
}

```

Returns the state of the internal relay.

### Attributes ###

|    Attribute    | Type |                                         Description                                          |
|-----------------|------|----------------------------------------------------------------------------------------------|
|     `ison`      | bool |                           Whether the channel is turned ON or OFF                            |
|   `has_timer`   | bool |                     Whether a timer is currently armed for this channel                      |
| `timer_started` |number|           Unix timestamp of timer start; `0` if timer inactive or time not synced            |
|`timer_duration` |number|                                     Timer duration, `s`                                      |
|`timer_remaining`|number|**experimental** If there is an active timer, shows seconds until timer elapses; `0` otherwise|
|   `overpower`   | bool |                         Whether an overpower condition has occurred                          |
|   `is_valid`    | bool |                                Whether power result is valid                                 |
|    `source`     |string|                               Source of the last relay command                               |

### Parameters ###

|Parameter| Type |                                               Description                                               |
|---------|------|---------------------------------------------------------------------------------------------------------|
| `turn`  |string|Accepted values are `on`, `off`. This will turn ON/OFF the respective output channel when request is sent|
| `timer` |number|                                  A one-shot flip-back timer in seconds                                  |

Shelly 3EM: `/emeter/{index}`
----------

```
GET /emeter/0

{
    "power": 0,
    "pf": 0,
    "current": 0,
    "voltage": 0,
    "is_valid": true,
    "total": 0,
    "total_returned": 0
}

```

### Attributes ###

|   Attribute    | Type |                    Description                     |
|----------------|------|----------------------------------------------------|
|    `power`     |number|            Instantaneous power, `Watts`            |
|      `pf`      |number|            Power factor (dimensionless)            |
|   `current`    |number|                    Current, `A`                    |
|   `voltage`    |number|                RMS voltage, `Volts`                |
|   `is_valid`   | bool |Whether the associated meter is functioning properly|
|    `total`     |number|            Total consumed energy, `Wh`             |
|`total_returned`|number|            Total returned energy, `Wh`             |

### Parameters ###

|  Parameter   |Type|                                Description                                |
|--------------|----|---------------------------------------------------------------------------|
|`reset_totals`|any |When requested will reset `total` and `total_returned` energy counters to 0|

Shelly 3EM: `/emeter/{index}/em_data.csv`
----------

This provides an export of the data gathered by the device. For each measurement channel, a CSV file is generated with the following columns:

* Date/time UTC
* Active energy Wh
* Returned energy Wh

This will always contain data for the entire time range stored on the device.

Shelly 3EM: `/reset_data`
----------

```
GET /reset_data

{
    "reset_data": 1
}

```

When requested will reset all device data.
