* [](/)
* Changelog

Version: 1.0

Changelog
==========

All notable changes to Shelly Gen2+ API Docs will be reflected here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Unreleased
----------

**Available as `1.7.4-beta2`**

### Fixed ###

* [Matter](/gen2/ComponentsAndServices/Matter) Speed up subscription resumption retries for non-ICD devices
* [Matter](/gen2/ComponentsAndServices/Matter) Fix DNS-SD answer parsing
* [Matter](/gen2/ComponentsAndServices/Matter) Fix DAKs with leading zeroes
* [Matter](/gen2/ComponentsAndServices/Matter) Fix PartsList attribute in [Cover](/gen2/ComponentsAndServices/Cover) mode
* [Webhook](/gen2/ComponentsAndServices/Webhook) Do not populate device config for conditions if Matter is enabled and jsvars count is unsufficient
* [Webhook](/gen2/ComponentsAndServices/Webhook) Respect `active_between` configuration when time is set manually
* [BTHome](/gen2/DynamicComponents/BTHome/) Fix crashes due to button sensors migration from versions prior to 1.6
* [3EM Gen3](/gen2/Devices/Gen3/Shelly3EMG3) Fix energy scales
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Retry TRV Set/ClearOverride commands
* BL0942 power meters: Fix wrong reports
* System: Fix mbuf resizing

### Added ###

* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Add support for BLU H&T ZB
* [BTHome](/gen2/DynamicComponents/BTHome/) Add support for BLU Button Tough 1 ZB, BLU RC Button 4 ZB, BLU Wall Switch 4 ZB, BLU H&T ZB
* [PlugS Gen3](/gen2/Devices/Gen3/ShellyPlugSG3), [OutdoorPlugS Gen3](/gen2/Devices/Gen3/ShellyOutdoorPlugSG3) Add support for [BTHomeControl](/gen2/DynamicComponents/BTHome/BTHomeControl)

### Local web ###

### Fixed ###

* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Fix unwanted TRV target temperature calls when switching pages

[1.7.3] 2025-12-18
----------

### Fixed ###

* [PlugS Gen3](/gen2/Devices/Gen3/ShellyPlugSG3), [OutdoorPlugS Gen3](/gen2/Devices/Gen3/ShellyOutdoorPlugSG3), [AZ Plug](/gen2/Devices/Gen3/ShellyAZPlug) Improved output zero-cross synchronization

[1.7.1] 2025-09-24
----------

### Fixed ###

* [Scripting](/gen2/ComponentsAndServices/Script) Fix scopes when calling another script from eJS
* [LoRa Add-On](/gen2/Addons/ShellyLoRaAddon) Fix failing Add-On updates
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Fix crash when dissociating TRV from gateway
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Reduce TRV write attempts
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Reallocate space from application to FS to allow for increased TRV firmware size
* [Matter](/gen2/ComponentsAndServices/Matter) Fix excessive power measurement reports
* BL0942 zero-cross zynchronization: Fix fallback on missing zero-cross signal
* [Pro1PM](/gen2/Devices/Gen2/ShellyPro1PM) Drop wrong JTI entry from BLE MF data
* [WiFi](/gen2/ComponentsAndServices/WiFi) Implement connectivity checks with GW pings; force a disconnect if PK seems to be lost
* Bump min bootloader version to 1.0.2

[1.7.0] 2025-07-30
----------

note

Firmware version `1.7.0` is being rolled out in phases, not all devices will receive the update immediately.

### Added ###

* [Zigbee](/gen2/ComponentsAndServices/Zigbee) Expose pairing status; enable RPC pairing
* [WiFi](/gen2/ComponentsAndServices/WiFi) Add BSSID in status
* [BTHome](/gen2/DynamicComponents/BTHome/) Add sensors statuses in button event info
* Devices with BL0942 power meter chip (1 PM Gen3, 1PM Mini Gen3, 1PM Gen4, 1PM Mini Gen4, PlugS Gen3, Outdoor PlugS Gen3, Plus 1PM Mini, AZ Plug): Enable zero-cross synchronized output operation
* RPC-GATTS: Optimize sending small frames in both directions
* [BTHomeControl](/gen2/DynamicComponents/BTHome/BTHomeControl) The `BTHomeControl` component maintains mapping between [Shelly BLU devices](/docs-ble) and the outputs of a Shelly WiFi device ([Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover), [Light](/gen2/ComponentsAndServices/Light)), offering both offline and online learning procedure to link the controller (BLU device) and controlee (Shelly WiFi device).
* [Matter](/gen2/ComponentsAndServices/Matter) Add `Matter.FactoryReset` to only reset Matter settings
* [Cover](/gen2/ComponentsAndServices/Cover) Add venetian blinds commands to MQTT control

### Changed ###

* [Scripting](/gen2/ComponentsAndServices/Script) Track CPU usage, throttle BLE Scan results when \>25%
* Update IDF to 5.4.1
* Update LwIP to 2.2.1
* Refactor factory reset to use buildtime FS list
* [BLE](/gen2/ComponentsAndServices/BLE) Improve BLE scan deduplication
* [WiFi](/gen2/ComponentsAndServices/WiFi) Do not save last AP on mains-powered devices
* OTA: Use current date in boot state sequence
* Dynamic Components: Optimize storage
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM), [ProDimmer2PM](/gen2/Devices/Gen2/ShellyProDimmer2PM) Allow setting undervoltage protection down to 90V

### Fixed ###

* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) BTHome: Fix device rescue (e.g. after BluTRV bootloader update)
* [1 Gen4](/gen2/Devices/Gen4/Shelly1G4), [1PM Gen4](/gen2/Devices/Gen4/Shelly1PMG4), [1 Mini Gen4](/gen2/Devices/Gen4/ShellyMini1G4), [1PM Mini Gen4](/gen2/Devices/Gen4/ShellyMini1PMG4) Fix Wi-Fi 6 support
* [1PM Gen4](/gen2/Devices/Gen4/Shelly1PMG4), [1PM Mini Gen4](/gen2/Devices/Gen4/ShellyMini1PMG4), [2PM Gen4](/gen2/Devices/Gen4/Shelly2PMG4) [Zigbee](/gen2/ComponentsAndServices/Zigbee) Fix incorrect power measurement reports
* [2PM Gen4](/gen2/Devices/Gen4/Shelly2PMG4) [Zigbee](/gen2/ComponentsAndServices/Zigbee) Fix wrong device type (shutter -\> rollershade); fix crash on profile change when paired; fix device not appearing as new/unknown to coordinator on profile change (requires re-pairing); fix required restart when slat control is enabled; fix migration of profile settings when switching alternative firmwares
* [Matter](/gen2/ComponentsAndServices/Matter) Fix crash by DNSSD resolving only non-LL IPv6 addresses
* [Input](/gen2/ComponentsAndServices/Input) Fix erroneous emission of `triple_push` notification when more than 3 pushes occur
* [Light](/gen2/ComponentsAndServices/Light), [RGBW](/gen2/ComponentsAndServices/RGBW) Allow for decimal values for transition\_duration and toggle\_after for MQTT control
* Fix `cfg_rev` different from 0 after factory reset
* Gen4 devices: Allow switching to alternative firmware on beta stage
* Gen4 devices: Fix BLE signal strength regression
* [BLE](/gen2/ComponentsAndServices/BLE) Fix scan manager crashes
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Adjust parsing of configuration to recognize all formats
* [Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover) Adjust error checks in MQTT control
* [Webhook](/gen2/ComponentsAndServices/Webhook) Fix invocation of conditional hooks when condition is invalid
* [PlusRGBW PM](/gen2/Devices/Gen2/ShellyPlusRGBWPM) Fix false overvoltage errors
* Debug: Disable interrupts when dumping core
* [BLE](/gen2/ComponentsAndServices/BLE) Don't disable coexistence when BLE is disabled
* [Matter](/gen2/ComponentsAndServices/Matter) Fix misprovisioned devices
* System LED: Fix indication for network/factory reset
* [Scripting](/gen2/ComponentsAndServices/Script) Clean up scripts Stop()/HandleError() teardown
* RMT, DALI, LedStrip: Change clock source to XTAL
* [EM Gen3](/gen2/Devices/Gen3/ShellyEMG3) Fix incorrect readings with 80A CT clamps
* [Sensor Addon](/gen2/Addons/ShellySensorAddon) Fix crashes on removal of DS18B20 sensors
* [Cover](/gen2/ComponentsAndServices/Cover) Fix error messages in MQTT control
* [PlusRGBW PM](/gen2/Devices/Gen2/ShellyPlusRGBWPM) Fix crashes on overcurrent error
* [AZ Plug](/gen2/Devices/Gen3/ShellyAZPlug) Update FFS certificate chain
* [Cover](/gen2/ComponentsAndServices/Cover) Reduce event notifications load in scripting

### Local web ###

### Added ###

* [Schedule](/gen2/ComponentsAndServices/Schedule), [Webhook](/gen2/ComponentsAndServices/Webhook) Add quick button to duplicate already created schedule/webhook
* [KNX](/gen2/Integrations/KNX/KNXCover) Auto-focus following address field on delimiter key press (dot - `.` for individual address, and slash - `/` for group address)
* [Zigbee](/gen2/ComponentsAndServices/Zigbee) Show current status
* [Zigbee](/gen2/ComponentsAndServices/Zigbee) Add button to enable pairing mode
* [Cover](/gen2/ComponentsAndServices/Cover) Add warning on device setup to use the correct device profile
* [BluTRV](/gen2/Devices/Gen3/ShellyBluGwG3#blutrv) Add schedule action to set valve position
* Plugs: Add 'black' preset to color picker
* Debug: Add quick button to enable logs to Shelly UDP server
* Debug: Add device id to diagnostics filenames and append device info to logs
* [Matter](/gen2/ComponentsAndServices/Matter) Add Matter reset button

### Changed ###

* [1 Gen4](/gen2/Devices/Gen4/Shelly1G4), [1PM Gen4](/gen2/Devices/Gen4/Shelly1PMG4), [1 Mini Gen4](/gen2/Devices/Gen4/ShellyMini1G4), [1PM Mini Gen4](/gen2/Devices/Gen4/ShellyMini1PMG4) Add separate page for switching to alternative firmware (Matter/Zigbee)
* [Webhook](/gen2/ComponentsAndServices/Webhook) Refactor trigger/event and conditions creation flow and UI
* [Matter](/gen2/ComponentsAndServices/Matter) Update warning on factory reset
* PM protections: Remove wrong description
* Update to Svelte 4
* Gen4 devices: Redesign alternative firmware notifications styling

### Fixed ###

* [BluTRV](/gen2/Devices/Gen3/ShellyBluGwG3#blutrv) Fix incorrect active/inactive buttons in Boost Mode
* Config: Fix handling nested configs when object is set to `null`
* Authentication: Fix incorrect message for wrong password, when HomeAssistant ble proxy is enabled
* Fix power factor wrong unit prefix
* Debug: Fix reset to default of Shelly UDP logs server
* Plugs: Fix night mode brightness sliders
* Gen4 devices: Hide BTHome components in Zigbee mode
* Gen4 devices: Fix alternative firmwares UI when no stable version is available
* [WiFi](/gen2/ComponentsAndServices/WiFi) Fix disabling WiFi when AP config doesn't exist
* [Zigbee](/gen2/ComponentsAndServices/Zigbee) Fix Zigbee enable/disable
* [Cover](/gen2/ComponentsAndServices/Cover) Drop warning messages that only apply to Switch profile
* [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Add default transition duration range

[1.6.2] 2025-05-20
----------

### Fixed ###

* [PlusUni](/gen2/Devices/Gen2/ShellyPlusUni) Fix operation when multiple DS18B20 sensors are attached
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix crashes due to wrong usage of a stack variable
* [Scripting](/gen2/ComponentsAndServices/Script) Cleanup extensions when terminating
* [BLE](/gen2/ComponentsAndServices/BLE) Fix handling in-progress connection when disconnecting

### Local web ###

### Fixed ###

* [Modbus](/gen2/ComponentsAndServices/Modbus) Fix missing UI support for Gen4 devices

[1.6.1] 2025-05-07
----------

note

Firmware version `1.6.1` is being rolled out in phases, not all devices will receive the update immediately.

### Added ###

* [2PM Gen3](/gen2/Devices/Gen3/Shelly2PMG3) Add support for Matter window covering
* [1L Gen3](/gen2/Devices/Gen3/Shelly1LG3), [2L Gen3](/gen2/Devices/Gen3/Shelly2LG3) Add overcurrent protection

### Fixed ###

* [BTHome](/gen2/DynamicComponents/BTHome/) Fix virtual groups of BTHomeSensor components
* [BTHome](/gen2/DynamicComponents/BTHome/) Fix a crash when RPC call finshes when no longer connected

[1.6.0] 2025-04-30
----------

note

Firmware version `1.6.0` is being rolled out in phases, not all devices will receive the update immediately.

note

Firmware version `1.6.0` is not deployed for Shelly 2PM Gen3, this device will receive `1.6.1` as soon as possible.

### Added ###

* [Matter](/gen2/ComponentsAndServices/Matter) Add support for Shelly 1 Gen3, 1PM Gen3, 1 Mini Gen3, 1PM Mini Gen3
* [LoRa Add-On](/gen2/Addons/ShellyLoRaAddon) Add support for Shelly 1 Gen3, 1PM Gen3, EM Gen3, Dimmer 0/1-10V PM Gen3, D Dimmer Gen3, 1 Gen4, 1PM Gen4
* [Scripting](/gen2/ComponentsAndServices/Script) Add `ArrayBuffer` and `AES` for Gen3 and Gen4 devices
* [Cover](/gen2/ComponentsAndServices/Cover) Add `maintenance_mode` config property
* [Cover](/gen2/ComponentsAndServices/Cover) Add [KNX](/gen2/Integrations/KNX/KNXCover) support
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Report external [BluTRV](/gen2/Devices/Gen3/ShellyBluGwG3#blutrv) temperature at a regular interval
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Add `connected` flag to [BluTRV](/gen2/Devices/Gen3/ShellyBluGwG3#blutrv) status
* [Modbus](/gen2/ComponentsAndServices/Modbus) Add support for [Input](/gen2/ComponentsAndServices/Input) component
* [Modbus](/gen2/ComponentsAndServices/Modbus) Add support for Gen4 devices
* [Light](/gen2/ComponentsAndServices/Light), [RGBW](/gen2/ComponentsAndServices/RGBW) Add MQTT control
* [WiFi](/gen2/ComponentsAndServices/WiFi), [Ethernet](/gen2/ComponentsAndServices/Eth) Report IPv6 addresses in status
* [Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover) Add physical control locking (`in_locked` config property)
* Advertise shelly\_name.local DNS-SD name
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM), [ProDimmer2PM](/gen2/Devices/Gen2/ShellyProDimmer2PM) Start calibration on simultaneous buttons press
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM), [ProDimmer2PM](/gen2/Devices/Gen2/ShellyProDimmer2PM) Start calibration on first toggle-on

### Changed ###

* [BTHome](/gen2/DynamicComponents/BTHome/) Drop BTHomeSensor components for newly added BLU button devices, see additional notes [here](/gen2/DynamicComponents/BTHome/)
* Update timezones info
* [KNX](/gen2/Integrations/KNX/) Relax validation of individual address
* [BLE](/gen2/ComponentsAndServices/BLE) Support enabling and disabling without a restart
* [Scripting](/gen2/ComponentsAndServices/Script) Enhance BLE API, see additional notes [here](/gen2/Scripts/ShellyScriptLanguageFeatures#bluetooth-support)
* [HTTP](/gen2/ComponentsAndServices/HTTP) Bump `HTTP.Request` limits

### Fixed ###

* [BLE](/gen2/ComponentsAndServices/BLE) Explicitly close all connections when stopping
* [BLE](/gen2/ComponentsAndServices/BLE) Restart if stuck connecting/disconnecting
* [BLE](/gen2/ComponentsAndServices/BLE) Stop advertising if RPC is disabled and no other services are registered
* [Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover): Fix missing power/current/pf events when switch is turned off
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Fix incorrect `connected` notification (when device tries to connect to host with stopped MQTT broker, on disconnect, status change for successful connection is sent)
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Fix disconnects when subscribing to a topic above 230 chars
* [RPC](/gen2/General/RPCProtocol) Limit max request payloads
* [Zigbee](/gen2/ComponentsAndServices/Zigbee) Don't run Zigbee task when safe mode is active
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Fix ignored transition duration after power cycle
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Fix overpower and overcurrent defaults

### Local web ###

### Added ###

* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Menu to select algorithm
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Add connected state
* [Zigbee](/gen2/ComponentsAndServices/Zigbee) Auto-reboot on enable/disable
* [XMOD](/gen2/ComponentsAndServices/XMOD) Support for manufacturer field
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Manual control valve position when TRV is disabled
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Refine UI texts and capitalization for consistency and clarity
* [PlusI4](/gen2/Devices/Gen2/ShellyPlusI4), [I4 Gen3](/gen2/Devices/Gen3/ShellyI4G3): Allow creating actions for input type of switch
* [Matter](/gen2/ComponentsAndServices/Matter) Loading message on enabling
* [Matter](/gen2/ComponentsAndServices/Matter) Note for reduced script memory when matter is enabled
* XT1: Service version in firmware page
* Guard when trying to access config page of non-existing component
* [WiFi](/gen2/ComponentsAndServices/WiFi) Displaying the MAC address when the octet starts with zero
* Time/Location: Option to set current device time
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Human readable BLE RSSI labels
* Energy metering: Net metering view **beta**
* Energy metering: Total section in details screen in mono-phase profile
* Device clients in advanced aside menu
* [Sensor Addon](/gen2/Addons/ShellySensorAddon) Adding addon sensor causes error after page refresh

### Changed ###

* [Webhook](/gen2/ComponentsAndServices/Webhook) Rework summary card in overview page

### Fixed ###

* [KVS](/gen2/ComponentsAndServices/KVS) Key encoding in the URL
* XT1: Missing webhook on page refresh
* UDP: Wrong port validations
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Temperature wheel on dynamic enable/disable TRV
* [BTHomeSensor](/gen2/DynamicComponents/BTHome/BTHomeSensor) Issue with fetching bthome sensor from the config page
* [Ogemray25A](/gen2/Devices/PoweredByShelly/Ogemray25A) Manufacturer name
* Aside nav links on small mobile screens
* [PlusWallDimmer](/gen2/Devices/Gen2/ShellyPlusWallDimmer) Fix duplicated inputs in home page
* [BTHome](/gen2/DynamicComponents/BTHome/) Hide BTHome for Gen 4 devices in Zigbee mode

[1.5.1] 2025-03-18
----------

### Fixed ###

* Eco mode: Set default min frequency to 40 MHz (match eco mode implementation prior to 1.5.0)
* Eco mode: Turn off WiFi idle time by default (match eco mode implementation prior to 1.5.0)
* [BLE](/gen2/ComponentsAndServices/BLE) Restore BLE scan deduplication

[1.5.0] 2025-02-20
----------

### Added ###

* [Scripting](/gen2/ComponentsAndServices/Script) Add `Virtual.off(listener_id)` to remove event handler
* [Scripting](/gen2/ComponentsAndServices/Script) Add `Script.storage`
* [Scripting](/gen2/ComponentsAndServices/Script) Add `Script.id`
* [Scripting](/gen2/ComponentsAndServices/Script) Add `Shelly.getUptimeMs()`
* [Scripting](/gen2/ComponentsAndServices/Script) Add `Timer.getInfo()`
* [Scripting](/gen2/ComponentsAndServices/Script) Store last script crash error
* [WiFi](/gen2/ComponentsAndServices/WiFi) Make AP SSID user-configurable
* [Switch](/gen2/ComponentsAndServices/Switch) Add `active_power_change` and `active_power_measurement` webhooks
* [Switch](/gen2/ComponentsAndServices/Switch), [PM1](/gen2/ComponentsAndServices/PM1) Add reporting of all PM measurements to periodic energy reports
* [Switch](/gen2/ComponentsAndServices/Switch) Add power/energy `reverse` config property
* [Cover](/gen2/ComponentsAndServices/Cover) Add slat control (venetian blinds) support
* [BLE](/gen2/ComponentsAndServices/BLE) Add `BLE.CloudRelay.ListInfos`
* [BLE](/gen2/ComponentsAndServices/BLE) Use extended advertising/scanning on BLE5 capable targets (Extended scan results are blended into the rest of the results. Extended advertising is not supported for now.)
* [Sys](/gen2/ComponentsAndServices/Sys#status) Add `btrelay_rev` to `sys.status`
* [Sys](/gen2/ComponentsAndServices/Sys#status) Add `last_sync_ts` to `sys.status`
* Add component attributes (for now, attributes, if any exist, are only shown in the response of `Shelly.GetComponents`)
* Add `keys` argument to `Shelly.GetComponents`
* Reintroduce safe mode
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM), [ProEM](/gen2/Devices/Gen2/ShellyProEM) Add `EMData|EM1Data.GetNetEnergies`
* [HT Gen3](/gen2/Devices/Gen3/ShellyHTG3) Add AM/PM mode for clock
* [XMOD](/gen2/ComponentsAndServices/XMOD) Add JWT payload to Shelly device info
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Add `blutrv.temperature_change` and `blutrv.position_change` webhook types to BluTRV component
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Add position, target temperature, current temperature and errors to BluTRV component status
* OTA: Allow updates without app and/or FS
* OTA: Swap slots if required for an update to succeed
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM), [ProDimmer2PM](/gen2/Devices/Gen2/ShellyProDimmer2PM) Add light [`range_map`](/gen2/ComponentsAndServices/Light#configuration)
* [ProDimmer 0/1-10V PM](/gen2/Devices/Gen2/ShellyProDimmer0110VPM) Add `Light.DimUp`, `Light.DimDown`, `Light.DimStop`
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Add [KNX](/gen2/Integrations/KNX/) support
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Start calibration on simultaneous buttons press
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Start calibration automatically on a new/factory reset device on the first toggle on
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3), [Dimmer 0/1-10V PM](/gen2/Devices/Gen3/ShellyDimmer0110VPMG3), [Plus 0-10V Dimmer](/gen2/Devices/Gen2/ShellyPlus10V): Add factory reset from input

### Removed ###

* [BLE](/gen2/ComponentsAndServices/BLE) Remove `ble.config.observer`

### Changed ###

* [Scripting](/gen2/ComponentsAndServices/Script) Enable let scoping
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Do not allow setting NaN with `Number.Set`
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Only accept boolean `true` or `false` for the `value` argument of `Boolean.Set`
* [Light](/gen2/ComponentsAndServices/Light) In single button mode, assign dim up/down direction depending on current brightness
* [BLE](/gen2/ComponentsAndServices/BLE) Optimize observer scan options
* [KVS](/gen2/ComponentsAndServices/KVS) Paginate `KVS.GetMany`. fix matching
* [WiFi](/gen2/ComponentsAndServices/WiFi) `Wifi.Scan`: Return up to 20 results; Filter out APs with RSSI \<= 85; Filter out hidden network APs; For each SSID only one AP with the best signal will be returned
* SNTP: change default server to time.cloudflare.com
* Update IDF to 5.2.2
* [Input.CheckExpression](/gen2/ComponentsAndServices/Input#inputcheckexpression), [Voltmeter.CheckExpression](/gen2/ComponentsAndServices/Voltmeter#voltmetercheckexpression) Limit number of inputs to 5
* [BTHome](/gen2/DynamicComponents/BTHome/) Increase BTHome device connect retries

### Fixed ###

* [Scripting](/gen2/ComponentsAndServices/Script) Refactor error handling, prevent execution in a doomed interpreter
* [Scripting](/gen2/ComponentsAndServices/Script) Fix `Shelly.removeEventHandler` crash when invoked inside the event handler itself
* [Scripting](/gen2/ComponentsAndServices/Script) Fix eJS induced crashes
* [BTHome](/gen2/DynamicComponents/BTHome/) BTHomeDevice: do not initiate connection only because of discovery
* [PM1](/gen2/ComponentsAndServices/PM1) Fix recovery from over-current/voltage/power errors
* [KVS](/gen2/ComponentsAndServices/KVS) Check for write errors when writing
* [Light](/gen2/ComponentsAndServices/Light), [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Reset auto-on/auto-off timer on `Set` requests
* [HTTP](/gen2/ComponentsAndServices/HTTP) client: Do not check content length on HEAD requests
* [Debug logs](/gen2/General/DebugLogs) Drop data when send buffer is full
* [BLE](/gen2/ComponentsAndServices/BLE) Fix failed scan start after software reboot
* [BLE](/gen2/ComponentsAndServices/BLE) Do not try to process queue if BT is not running
* SNTP: Randomize update interval
* OTA: Prevent premature commits
* OTA: Prevent sleep during OTA on battery-operated devices; don't allow OTA when battery is low
* ADE7953, ADE7880 power meters: Fix check for negative active power being smaller than apparent power
* Factory reset: Wipe old FS, scratch space, NVS, EM data partition
* [D Dimmer Gen3](/gen2/Devices/Gen3/ShellyDDimmerG3) Fix discovery of D4I/DALI 2 ECGs
* [EM Gen3](/gen2/Devices/Gen3/ShellyEMG3) Update EM1 component numbering to match shell print
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS) Fix spurious LED indication
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS) Fix failed night mode activation
* [2PM Gen3](/gen2/Devices/Gen3/Shelly2PMG3) Enable KNX
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) BluTRV: Fix incorrect `last_updated_ts` on reboot
* [XMOD](/gen2/ComponentsAndServices/XMOD) Ensure config is valid before applying
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Fix light transition duration after reboot
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Calibration and transition improvements
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) Fail calibration when a protection is triggered
* [Dimmer Gen3](/gen2/Devices/Gen3/ShellyDimmerG3) PM gains correction; synchronization fix
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Fir broken [BluTrv](/gen2/Devices/Gen3/ShellyBluGwG3#blutrv) webhooks
* [BLE](/gen2/ComponentsAndServices/BLE) Fix large advertisement data processing
* [Scripting](/gen2/ComponentsAndServices/Script) Prevent var leaks from interpreters
* [Scripting](/gen2/ComponentsAndServices/Script) Fix control of active eJS instance
* [Scripting](/gen2/ComponentsAndServices/Script) Fix enable attempts on already enabled scripts
* [Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover) Fix missing power measurement events when output if turned off
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Fix parsing of incoming messages fixed headers
* ADE7953, ADE7880 power meters: prevent main queue starvation
* BL0937 power meter: avoid division by zero
* Optimize Eco mode
* UART: drain RX from ISR context

### Local web ###

### Added ###

* [Scripting](/gen2/ComponentsAndServices/Script) Introduce all new functions and object methods to script editor autocompletion
* [Outbound Websocket](/gen2/ComponentsAndServices/Ws) Visual identification for outbound websocket connection in the status bar
* [Cover](/gen2/ComponentsAndServices/Cover) `Cover.Stop` action
* [Light](/gen2/ComponentsAndServices/Light), [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Add dim up and dim down fade rate for actions
* [BTHome](/gen2/DynamicComponents/BTHome/) Notification while BTHome scan is in progress
* Warning when the device doesn't have synced time
* Warning when a request takes too long
* Buttons to copy firmware version, web version and device identifications
* Debug: HTTP ping test to diagnostics page
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Setting for min valve position
* [Cover](/gen2/ComponentsAndServices/Cover)[Light](/gen2/ComponentsAndServices/Light) Popup message for calibration status

### Removed ###

* [Virtual Components](/gen2/DynamicComponents/Virtual/) Virtual group - script visual binding

### Changed ###

* [Schedule](/gen2/ComponentsAndServices/Schedule) Overview page update
* [WiFi](/gen2/ComponentsAndServices/WiFi) Setting Wi-Fi and AP pages update
* [Cover](/gen2/ComponentsAndServices/Cover) Error message when calibration fails due to exceeded movement time limit
* [Range extender](/gen2/ComponentsAndServices/WiFi#configuration) Clients page update
* Toggle after timer pill shows label instead of number when there are less than 3 seconds left
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Update bluetooth signal strength levels based on the feedback
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Refine texts consistency and clarity

### Fixed ###

* [Cover](/gen2/ComponentsAndServices/Cover) Multiple Go to position in Favorites exceeds the frame limits
* [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) The color picker "jumps" and cannot select a color for the action/schedule
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Wrong placeholder for server url and client id
* [Schedule](/gen2/ComponentsAndServices/Schedule) Selected day is always shown as Sunday when created from other client
* [Schedule](/gen2/ComponentsAndServices/Schedule) Check for supported actions in schedules
* [Schedule](/gen2/ComponentsAndServices/Schedule) Not needed step of selecting component when creating new schedule
* [KNX](/gen2/Integrations/KNX/) Hide inputs menu if no input components are presented
* [Scripting](/gen2/ComponentsAndServices/Script) Error trace in debug console
* [Sensor Addon](/gen2/Addons/ShellySensorAddon) IO settings for inputs from SensorAddon are missing
* [Light](/gen2/ComponentsAndServices/Light) Fix duplicated inputs in home page
* Energy values rounding to 3 decimal places
* Typerror when toggle\_after action is created, while the device doesn't have synced time
* Show correct values when night mode and button presets are changed
* Error when loading timezones and current tz is null
* Human readable name when sensor from addon do not have value
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Update TRV sensor data also when display value is updated
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Adding sensor causes error when sensor is not yet initialized
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Edge case where the position is not reflected correctly
* [BLU Gateway Gen3](/gen2/Devices/Gen3/ShellyBluGwG3) Redirect to home page after a successful pairing
* [Plus1PM](/gen2/Devices/Gen2/ShellyPlus1PM) Fix missing active energy total
* [XMOD](/gen2/ComponentsAndServices/XMOD) Format the jwt token before sending
* [ProEM](/gen2/Devices/Gen2/ShellyProEM) Apparent power readings (VA) from Clamp A are displayed on both channels in Diagram View
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Diagram view values are not reactive in monophase profile
* [PlusUni](/gen2/Devices/Gen2/ShellyPlusUni) Opening examples in custom expression toggles a save action
* [PlusUni](/gen2/Devices/Gen2/ShellyPlusUni) Wrong link for count threshold page on input card
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Button for downloading em data
* [ProRGBWWPM](/gen2/Devices/Gen2/ShellyProRGBWWPM) Fix missing voltage and power pills
* Some links in the aside nav bar are hidden on smaller screens

[1.4.5] 2024-10-17
----------

### Fixed ###

* [HT Gen3](/gen2/Devices/Gen3/ShellyHTG3) Fix unresponsive devices

[1.4.4] 2024-10-17
----------

### Fixed ###

* mbedtls: Fix defragmentation of input handshake messages
* [RPC](/gen2/General/RPCProtocol) Ensure that next generated ID is distinct from previous
* [RPC](/gen2/General/RPCProtocol) Drop responses that cannot be delivered
* [Scripting](/gen2/ComponentsAndServices/Script) Orderly shutdown of scripts on reboot
* [Scripting](/gen2/ComponentsAndServices/Script) Fix MQTT handlers cleanup when script is removed
* `Pro` devices: Fix unintentional `Wi-Fi` LED color change when `Reset` button is pressed briefly
* [PlusRGBW PM](/gen2/Devices/Gen2/ShellyPlusRGBWPM) Fix input `invert` property
* [HTTP.GET](/gen2/ComponentsAndServices/HTTP#httpget) Fix `timeout` argument

### Changed ###

* OTA: auto-commit updates and impose minimum required commit timeout

### Local web ###

### Fixed ###

* [Cover](/gen2/ComponentsAndServices/Cover) Favorites buttons don't fit on single line

[1.4.3] 2024-08-22
----------

### Fixed ###

* [ProEM](/gen2/Devices/Gen2/ShellyProEM), [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix status response when non-critical errors are present

[1.4.2] 2024-08-19
----------

### Fixed ###

* Fix mDNS resolution failures (use correct length when adding NSEC data, fix mangled IP address in delayed sends)
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM), [ProDimmer2PM](/gen2/Devices/Gen2/ShellyProDimmer2PM) Fix overpower protection trip during calibration
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM), [ProDimmer2PM](/gen2/Devices/Gen2/ShellyProDimmer2PM)Fix recognition of non-dimmable loads
* [Scripting](/gen2/ComponentsAndServices/Script) Fix [Virtual.getHandle](/gen2/Scripts/ShellyScriptLanguageFeatures#virtualgethandlekey) crashes
* [XMOD](/gen2/ComponentsAndServices/XMOD) Fix inconsistent JWS handling

[1.4.1] 2024-07-31
----------

### Fixed ###

* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) Fix notifications to backend

[1.4.0] 2024-07-31
----------

note

`1.3.3` is a mandatory update before `1.4.0`. Devices running versions older than `1.3.3` will not be served `1.4.0`.

### Added ###

* [KNX Integration](/gen2/Integrations/KNX/)
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) [Webhooks](/gen2/ComponentsAndServices/EM#webhook-events) for `total_current_change`, `total_active_power_change`, `total_apparent_power_change`
* [ProEM](/gen2/Devices/Gen2/ShellyProEM), [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) [CT types](/gen2/ComponentsAndServices/EM#emgetcttypes) support
* [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Option to use current `brightness`, `white` and `rgb` values in `button_presets` and `night_mode` [configuration](/gen2/ComponentsAndServices/RGB#configuration)
* [Light](/gen2/ComponentsAndServices/Light), [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) `offset` argument in [`Set`](/gen2/ComponentsAndServices/Light#lightset) method
* [Light](/gen2/ComponentsAndServices/Light), [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) [DimUp](/gen2/ComponentsAndServices/Light#lightdimup), [DimDown](/gen2/ComponentsAndServices/Light#lightdimdown), [DimStop](/gen2/ComponentsAndServices/Light#lightdimstop) methods
* Pro devices: emit `sys_btn_down`, `sys_btn_up`, `sys_btn_push` [notifications](/gen2/ComponentsAndServices/Sys#notifications) from user button
* Pro devices: [`sys_btn_toggle`](/gen2/ComponentsAndServices/Sys#configuration) config option to control outputs from user button
* Pro devices: [Virtual Components](/gen2/DynamicComponents/Virtual/) and [BTHome](/gen2/DynamicComponents/BTHome/)
* [BluGw](/gen2/Devices/Gen2/ShellyBluGw) [`sys_led_enable`](/gen2/Devices/Gen2/ShellyBluGw#blugw) toggle
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Optional `id` argument in [`Virtual.Add`](/gen2/DynamicComponents/Virtual/)
* [BTHome](/gen2/DynamicComponents/BTHome/) Optional `id` argument in [`BTHome.AddSensor`](/gen2/DynamicComponents/BTHome/) and [`BTHome.AddDevice`](/gen2/DynamicComponents/BTHome/)
* [PlusPM Mini](/gen2/Devices/Gen2/ShellyPlusPMMini), [PM Mini](/gen2/Devices/Gen3/ShellyMiniPMG3) [`reverse`](/gen2/ComponentsAndServices/PM1#configuration) config option in PM1 component
* [PlusRGBW PM](/gen2/Devices/Gen2/ShellyPlusRGBWPM) [`hf_mode`](/gen2/Devices/Gen2/ShellyPlusRGBWPM#plusrgbwpm) toggle
* Use both cloud an generic CA bundle for cloud conenction and update checks
* [IPv6](/gen2/General/IPv6) Devices will attempt to obtain a public address using the Neighbour Discovery Protocol. If successful, this address can then be used to reach a Shelly device on the network, and device will include it in MDNS host advertisements.
* [Scripting](/gen2/ComponentsAndServices/Script) [`Virtual`](/gen2/Scripts/ShellyScriptLanguageFeatures#virtual-apis) APIs
* [WiFi](/gen2/ComponentsAndServices/WiFi) Add support for WPA3

### Fixed ###

* [BLE Scanner](/gen2/Scripts/ShellyScriptLanguageFeatures#blescanner) Fix lifetime issues
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Require restart when [`use_client_cert`](/gen2/ComponentsAndServices/Mqtt#configuration) is changed
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Allow more than one outstanding publish request (avoid MQTT queue overflows)
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix crash on [phase-to-phase calibration](/gen2/ComponentsAndServices/EM#emphasetophasecalib)
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix recovery from [`power_meter_failure`](/gen2/ComponentsAndServices/EM#status) error
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix [`reverse`](/gen2/ComponentsAndServices/EM#configuration) CT measurement in `monophase` profile
* [PlusPM Mini](/gen2/Devices/Gen2/ShellyPlusPMMini), [Plus1PM Mini](/gen2/Devices/Gen2/ShellyPlus1PM), [PM Mini](/gen2/Devices/Gen3/ShellyMiniPMG3), [1PM Mini](/gen2/Devices/Gen3/ShellyMini1PMG3) Fix incorrect frequency reports
* [Scripting](/gen2/ComponentsAndServices/Script) Fix create/call ejs script from other script
* [Ethernet](/gen2/ComponentsAndServices/Eth) Fix updating [config](/gen2/ComponentsAndServices/Eth#configuration) parameters for `static` mode
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Fix counting of vcs without an owner
* HTTP: Fix processing of zero-length responses
* [BLE](/gen2/ComponentsAndServices/BLE) Do not attempt to advertise if BT is not running
* [BLE](/gen2/ComponentsAndServices/BLE) Update bt-common to fix a UAF in scan results processing
* [Debug logs](/gen2/General/DebugLogs) Fix websocket authentication

### Changed ###

* Update IDF to 5.2.1
* Convert ca.pem to binary; ship full CA bundle on Gen3 devices
* Update mbedtls to 3.5.2
* Repartition all 4M devices to reallocate 64K from FS to app
* Fix PT location for Gen3 devices
* [Shelly.ListTimezones](/gen2/ComponentsAndServices/Shelly#shellylisttimezones) Paginate response **BREAKING CHANGE**
* [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Replace HTTP endpoint `/light/{id}` with [`/color/{id}`](/gen2/ComponentsAndServices/RGBW#http-endpoint-colorid) **BREAKING CHANGE**
* [Light](/gen2/ComponentsAndServices/Light), [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Apply night mode regardless of current brightness
* [Light](/gen2/ComponentsAndServices/Light), [RGB](/gen2/ComponentsAndServices/RGB), [RGBW](/gen2/ComponentsAndServices/RGBW) Do not apply `min_brightness_on_toggle` when night mode is active
* [XMOD](/gen2/ComponentsAndServices/XMOD) Change default LED type to plain

### Removed ###

* [WiFi](/gen2/ComponentsAndServices/WiFi) Drop support for WPA

### Local web ###

### Added ###

* [KNX](/gen2/Integrations/KNX/) configuration pages
* [WiFi](/gen2/ComponentsAndServices/WiFi) connection status and failure reason
* [BluGw](/gen2/Devices/Gen2/ShellyBluGw) system LED enable/disable
* [Virtual Components](/gen2/DynamicComponents/Virtual/) and [BTHome](/gen2/DynamicComponents/BTHome/) for Pro devices
* Show [BTHome](/gen2/DynamicComponents/BTHome/) devices on dashboard
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) actions based on total values
* Button to enable the websocket [debug log](/gen2/General/DebugLogs)
* Device name in the tab title
* Pro devices: option to control outputs from user button

### Fixed ###

* [Schedule](/gen2/ComponentsAndServices/Schedule) editor crash when invalid body is saved via RPC
* Invalid status for the second [WiFi](/gen2/ComponentsAndServices/WiFi) when only the first one is configured
* [Cover](/gen2/ComponentsAndServices/Cover) slider not reactive sometimes
* [BTHome](/gen2/DynamicComponents/BTHome/) information initial fetch
* [BTHome](/gen2/DynamicComponents/BTHome/) filter only supported webhooks
* Section contents do not update when changing component type in URL
* Input field deleting decimals
* [Cover](/gen2/ComponentsAndServices/Cover) obstacle detection can not be configured
* [Cover](/gen2/ComponentsAndServices/Cover) auto-recovery can not be configured
* [Cover](/gen2/ComponentsAndServices/Cover) fix incorrect "position lost" message when cover is closed
* RPC over UDP can not be configured
* [ProEM](/gen2/Devices/Gen2/ShellyProEM) actions can not be created
* Display detached inputs for [Light](/gen2/ComponentsAndServices/Light)
* Creating option for [VirtualComponents::Enum](/gen2/DynamicComponents/Virtual/Enum) is not possible sometimes
* [PlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) LED indicator settings can not be configured
* [Pro4PM](/gen2/Devices/Gen2/ShellyPro4PM), [ProDualCoverPM](/gen2/Devices/Gen2/ShellyProDualCoverPM) Fix missing display settings
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix missing add-on card
* [ProEM](/gen2/Devices/Gen2/ShellyProEM), [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) [CT types](/gen2/ComponentsAndServices/EM#emgetcttypes) Fix error handling
* Rework diagnostics button for debug log and device data

### Changed ###

* Unify behavior on setting page save
* Unify split button
* Rework status bar
* Trigger auto detect location via button
* Load timezones list on setting page open
* AP and Range extender configuration page rework
* Rework script editor page
* Improve [PlusRGBW PM](/gen2/Devices/Gen2/ShellyPlusRGBWPM) color picker

[1.3.3] 2024-06-25
----------

### Fixed ###

* [Analog Input](/gen2/ComponentsAndServices/Input) Fix wrong values after reboot
* shelly\_cloud.pem: Add roots for popular cloud service providers
* mbedtls: Fix stack overflow caused by ECP optimization
* [Dimmer 0/1-10V PM](/gen2/Devices/Gen3/ShellyDimmer0110VPMG3) Fix sensor add-on with DHT22

[1.3.2] 2024-05-22
----------

### Fixed ###

* LWIP: fix support of MDNS queries (resolving `.local` names)

### Added ###

* OTA: bootloader descriptor for detecting BL versions

[1.3.1] 2024-04-30
----------

### Fixed ###

* [Sensor Addon](/gen2/Addons/ShellySensorAddon) Verify DS18B20 CRC when reading sensor data
* [Plus1PM Mini](/gen2/Devices/Gen2/ShellyPlus1PM), [PlusPM Mini](/gen2/Devices/Gen2/ShellyPlusPMMini), [1PM Mini](/gen2/Devices/Gen3/ShellyMini1PMG3), [PM Mini](/gen2/Devices/Gen3/ShellyMiniPMG3) Fix BL0942 energy sign calculation
* [Voltmeter](/gen2/ComponentsAndServices/Voltmeter) Fix `xvoltage` value in event payload
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Fix loading scales after reboot

### Changed ###

* [PlusUni](/gen2/Devices/Gen2/ShellyPlusUni) Decrease lower limit of [voltmeter](/gen2/ComponentsAndServices/Voltmeter) `report_thr`

[1.3.0] 2024-04-25
----------

### Fixed ###

* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Incorrect power factor calculation
* [PlusWallDimmer](/gen2/Devices/Gen2/ShellyPlusWallDimmer) WiFi LED turns on/off unexpectedly
* [Pro4PM](/gen2/Devices/Gen2/ShellyPro4PM) Eliminate use of stale/uninitialized timer IDs
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM) Fix dimming at range limit; fix calibration crash
* [Pro1PM](/gen2/Devices/Gen2/ShellyPro1PM), [Pro2PM](/gen2/Devices/Gen2/ShellyPro2PM), [Pro4PM](/gen2/Devices/Gen2/ShellyPro4PM), [ProDualCoverPM](/gen2/Devices/Gen2/ShellyProDualCoverPM), [Plus2PM](/gen2/Devices/Gen2/ShellyPlus2PM) Zero-cross synchronizer crash on device init
* [Scripting](/gen2/ComponentsAndServices/Script) Fix ejs ExecFile monitor
* [Scripting](/gen2/ComponentsAndServices/Script) Add 500ms delay before starting scripts on boot
* [Scripting](/gen2/ComponentsAndServices/Script) Fix ejs\_event varleak
* [Scripting](/gen2/ComponentsAndServices/Script) Long print() output is printed halfway
* [Scripting](/gen2/ComponentsAndServices/Script) ejs\_http: return 429 (Too Many Requests) when there are too many requests in flight
* [Scripting](/gen2/ComponentsAndServices/Script) Fix BLE scanner crash
* [Scripting](/gen2/ComponentsAndServices/Script) Fix ejs\_set\_tzoffset() and ejs validation checks
* [Light](/gen2/ComponentsAndServices/Light) Fix transition notifications
* [Light](/gen2/ComponentsAndServices/Light) HTTP compatibility does not perform toggle
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Handle stale DNS resolution callback
* [WiFi](/gen2/ComponentsAndServices/WiFi) Suppress disconnected/connecting flapping notifications
* LFS: lfs\_superblock\_t is not always located at a constant offset
* LFS: Add an assertion that block 0 and 1 are never allocated during normal operation
* LFS: Fix superblock expansion
* DNS-DS: Fix deadlock between main and tcpip tasks
* HTTP: Fix SendWebSocketFrame recursion
* RPC: Reject request in case of authz error
* Fix base64 decode buffer overflow when decoding a padded output
* Geolocation is not saved correctly
* System LED: missing response to WiFi disconnects
* HTTP POST: send 400 in response to bad requests

### Added ###

* [PlusI4 and PlusI4 DC](/gen2/Devices/Gen2/ShellyPlusI4): [Input.Trigger](/gen2/ComponentsAndServices/Input#inputtrigger) RPC to simulate events from physical inputs
* [Virtual Components::Button](/gen2/DynamicComponents/Virtual/Button)
* [BTHome Observer and Components](/gen2/DynamicComponents/BTHome/)
* Add DigiCert Global Root G3 certificate (used by Azure Event Grid)

### Changed ###

* [WiFi](/gen2/ComponentsAndServices/WiFi) Use 20MHz-wide channels for AP mode
* Restore timezone aliases (previously removed in `1.0.0`)
* Optimize shos event dispatch to improve the performance of event delivery
* Refactor LwIP
* [Modbus](/gen2/ComponentsAndServices/Modbus) Replace esp-modbus with nanoMODBUS
* [EM](/gen2/ComponentsAndServices/EM), [EM1](/gen2/ComponentsAndServices/EM1), [PM1](/gen2/ComponentsAndServices/PM1), [Switch](/gen2/ComponentsAndServices/Switch) Throttle status change notifications when cloud is enabled
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Reduce rate limit capacity to 30

### Local web ###

### Added ###

* [Virtual Components](/gen2/DynamicComponents/Virtual/) Add virtual button and drop virtual boolean(view=button)
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Auto generate script and bind it to virtual group *beta*
* [BTHome Components](/gen2/DynamicComponents/BTHome/)
* Show a site-wide message or highlighted icon when there is a new stable version available

### Fixed ###

* [ProDualCoverPM](/gen2/Devices/Gen2/ShellyProDualCoverPM) Fix duplicated first channel
* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) The smoke alarm cannot be muted with web button
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM) Unreasonable amount of calibrate buttons
* [PM Mini Gen3](/gen2/Devices/Gen3/ShellyMiniPMG3) TypeError when creating webhook
* [PlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Night mode can not be activated
* [BLU Gateway](/gen2/Devices/Gen2/ShellyBluGw) Menu for actions & schedule is visible
* [Webhook](/gen2/ComponentsAndServices/Webhook) Fix `undefined` bug when loading supported webhook types
* [Ethernet](/gen2/ComponentsAndServices/Eth) Fix `gw` input settings
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Checkbox for enable MQTT control is missing
* [Schedule](/gen2/ComponentsAndServices/Schedule) Wrong minutes schedule in Firefox
* [Scripting](/gen2/ComponentsAndServices/Script) Script editor crashes when too many brackets are opened
* [Scripting](/gen2/ComponentsAndServices/Script) Fix inserting second snippet
* Inconsistent warning text for actions not matching input mode
* Power protections: updated number precision and descriptions; fixed some missing inputs
* Visual updates and fixed reactivity of some inputs
* Download diagnostics button blind spot
* Local web doesn't load on ios 16 or older
* Auto off/on timers can not be disabled

### Changed ###

* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT), [HT Gen3](/gen2/Devices/Gen3/ShellyHTG3) Unite settings
* Force [Shelly.CheckForUpdate](/gen2/ComponentsAndServices/Shelly#shellycheckforupdate) when loading route /settings/firmware
* Rework the [KVS](/gen2/ComponentsAndServices/KVS) pages
* [Scripting](/gen2/ComponentsAndServices/Script) Optimize scripts cards
* Optimize new action calls

[1.2.3] 2024-02-28
----------

### Fixed ###

* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS) Wrong device id

[1.2.2] 2024-02-23
----------

### Fixed ###

* [Scripting](/gen2/ComponentsAndServices/Script) Missing `print()` output

[1.2.1] 2024-02-22
----------

### Fixed ###

* Troublesome Wi-Fi reconnects

[1.2.0] 2024-02-13
----------

### Fixed ###

* [Plus1 Mini](/gen2/Devices/Gen2/ShellyPlus1), [Plus1PM Mini](/gen2/Devices/Gen2/ShellyPlus1PM), [1 Mini](/gen2/Devices/Gen3/ShellyMini1G3), [1PM Mini](/gen2/Devices/Gen3/ShellyMini1PMG3) Persist output state on soft reboot
* `aenergy`, `ret_aenergy` and `counts` accumulators: `minute_ts` value is incorrect
* Crash when core dumps are disabled but logs are enabled
* DNS-SD reconfiguration fails to remove services
* [ProDimmer1PM](/gen2/Devices/Gen2/ShellyProDimmer1PM) Status LED doesn't blink when user button is held down for 5+ seconds
* [PM1](/gen2/ComponentsAndServices/PM1) `power_update` event notifications are not emitted
* LFS doesn't perform write-leveling when 50+% full
* [Input](/gen2/ComponentsAndServices/Input) Rework calculation of `counts.xby_minute` values
* [Bluetooth Low Energy](/gen2/ComponentsAndServices/BLE) Optimize scan event queue
* [Virtual Components](/gen2/DynamicComponents/Virtual/) Webhooks associated with virtual components are not deleted when component is removed
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Incorrect PUBLISH packet ID parsing
* Dynamic components storage: adjust line size calculation when updating record
* Incomplete core dumps written to flash

### Added ###

* [Sys](/gen2/ComponentsAndServices/Sys) `component_added` and `component_removed` event notifications
* [EMData](/gen2/ComponentsAndServices/EMData), [EM1Data](/gen2/ComponentsAndServices/EM1Data) `ResetCounters` RPC methods

### Changed ###

* [EM](/gen2/ComponentsAndServices/EM), [EM1](/gen2/ComponentsAndServices/EM1) Initialize component with error if power meter chip failed to start
* [VirtualComponents::Boolean](/gen2/DynamicComponents/Virtual/Boolean) Drop webhook types `boolean.true` and `boolean.false` in favor of `boolean.change`
* [VirtualComponents](/gen2/DynamicComponents/Virtual/) Add `meta` object in config (note: former `ui` object is nested into `meta.ui`)
* [Schedule](/gen2/ComponentsAndServices/Schedule) Round sunrise and sunset event times to whole minute
* Improved OTA mechanism: move commit state to OTA data and revert handling to bootloader

### Removed ###

* [Light](/gen2/ComponentsAndServices/Light) Drop `default.brightness` from configuration (deprecated since `1.0.0`)
* [Plus 0-10V Dimmer](/gen2/Devices/Gen2/ShellyPlus10V) Disable `eco_mode`

### Local web ###

### Fixed ###

* WiFi connected status is not reactive
* Crash when schedule is created via script/rpc
* Missing webhook action for Analog inputs
* Remove unsupported settings from Pro addon
* Analog values are not reactive
* Schedules and actions no longer ask for active component when active component is only one
* Power protections messages
* PlugS and PlugUK night mode
* Missing button for virtual boolean toggle view
* Show password visiblity toggle
* Webhook editor type error for EM1

### Added ###

* Enable/disable Plus Addon
* Enable auto update firmware

### Changed ###

* Improve modal dialog
* Improve message on profile change
* Sensors and Plus Addon UI rework
* Improve script errors
* Input range map calibration rework
* Improve color wheel
* Component overview pages rework
* Use the same style for pages without items
* Tweaks to the webhook and schedules creation page
* Message for not supported schedules jobs via the embedded editor

[1.1.1] 2024-01-05
----------

### Fixed ###

* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT) Fix regression in humidity offset for production batch 2220-Broadwell

[1.1.0] 2023-12-19
----------

### Added ###

* [Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover), [PM1](/gen2/ComponentsAndServices/PM1) `ResetCounters` RPC method to reset persistent energy accumulators
* [Switch](/gen2/ComponentsAndServices/Switch) Separate accumulator for returned energy (`ret_aenergy`)
* [Switch](/gen2/ComponentsAndServices/Switch), [Cover](/gen2/ComponentsAndServices/Cover) Persist energy counters on power loss
* [Switch](/gen2/ComponentsAndServices/Switch) Input mode `activate`
* [Input](/gen2/ComponentsAndServices/Voltmeter) (in `analog` mode), [Voltmeter](/gen2/ComponentsAndServices/Voltmeter) `xvalue` support: allow raw value transformations by a user-provided JS expression
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) with [addon](/gen2/Addons/ShellyProOutputAddon) and [ProEM](/gen2/Devices/Gen2/ShellyProEM) Modbus TCP control of [Switch](/gen2/ComponentsAndServices/Switch#modbus-registers)
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) `triphase` and `monophase` profiles
* [Scripting MQTT support](/gen2/Scripts/ShellyScriptLanguageFeatures/#mqtt-support) `MQTT.subscribe()`: wildcard topics

### Fixed ###

* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Erroneous power factor and frequency reports when load is disconnected
* [ProEM](/gen2/Devices/Gen2/ShellyProEM) `total_act_ret_energy` is not recorded
* [Cover](/gen2/ComponentsAndServices/Cover) Restore current position in case device crashes
* [Cover](/gen2/ComponentsAndServices/Cover) Reduce power meters load to improve stability; autorecover unresponsive power meters
* [Cover](/gen2/ComponentsAndServices/Cover) Fix calibration procedure for motors with adjustable travel modes (fast/slow)
* [Pro1PM](/gen2/Devices/Gen2/ShellyPro1PM), [Pro2PM](/gen2/Devices/Gen2/ShellyPro2PM), [Pro4PM](/gen2/Devices/Gen2/ShellyPro4PM), [ProDualCoverPM](/gen2/Devices/Gen2/ShellyProDualCoverPM), [Plus2PM](/gen2/Devices/Gen2/ShellyPlus2PM) Zero-cross synchronizer crashes on boot
* [Light](/gen2/ComponentsAndServices/Light) Do not apply `min_brightness_on_toggle` when [`Light.Set`](/gen2/ComponentsAndServices/Light#lightset) is invoked with `transition_duration` argument
* [Light](/gen2/ComponentsAndServices/Light) Fix night mode activation
* [Light](/gen2/ComponentsAndServices/Light) Initial state `restore_last` is not applied
* [Input](/gen2/ComponentsAndServices/Input) Fix validation of [`Input.SetConfig`](/gen2/ComponentsAndServices/Input#inputsetconfig) `type` argument
* [MQTT](/gen2/ComponentsAndServices/Mqtt) `ssl_ca` property is not present in [`MQTT.GetConfig`](/gen2/ComponentsAndServices/Mqtt#mqttgetconfig) response
* DNS-SD: Fix interface matching when v4 or v6 is disabled
* Fix AP & BLE reset from user button
* [HTTP](/gen2/ComponentsAndServices/HTTP) Crash when there is no data following parsed header

### Changed ###

* [Scripting MQTT support](/gen2/Scripts/ShellyScriptLanguageFeatures/#mqtt-support) `MQTT.subscribe()`: throw exception instead of aborting script if invocation fails; `MQTT.publish()`: change return type to `boolean`

### Local web ###

### Added ###

* Support returned energy accumulators
* Support consumed/returned energy accumulators reset

### Fixed ###

* Addons are missing on Plus series
* HTTP request doesn't work properly
* Drop duplicated settings for PlusHT
* Optimize countdown timers visualization
* Optimize schedules editing
* Delete action icons are misaligned
* Actions and schedules can be accidentally deleted
* [Bluetooth Low Energy Gateway](/gen2/Devices/Gen2/ShellyBluGw) Missing scripts and range extender

[1.0.8] 2023-11-06
----------

### Fixed ###

* [Webhook](/gen2/ComponentsAndServices/Webhook) Fix handling of HTTP compatibility loopback calls

### Local web ###

### Fixed ###

* Idle settings page on Pro2PM in cover profile
* Tooltip on devices displays ethernet disabled when ethernet is enabled

[1.0.7] 2023-10-31
----------

### Changed ###

* Reworked mDNS responder
* Improve bootloader update

### Removed ###

* [PlusPM Mini](/gen2/Devices/Gen2/ShellyPlusPMMini) Remove no-load condition
* [Scripting](/gen2/Scripts/ShellyScriptLanguageFeatures#resource-limits) Remove 15kB limit on script size

### Added ###

* [Plus2PM](/gen2/Devices/Gen2/ShellyPlus2PM), [Pro2](/gen2/Devices/Gen2/ShellyPro2), [Pro2PM](/gen2/Devices/Gen2/ShellyPro2PM) Add [cycle mode](/gen2/ComponentsAndServices/Switch) support
* [Input](/gen2/ComponentsAndServices/Input) Configuration property `enable`

### Fixed ###

* [BLE](/gen2/ComponentsAndServices/BLE) MAC in BLE MFD is in the wrong endianness
* [MQTT](/gen2/ComponentsAndServices/Mqtt) Fix parsing of fragmented messages
* [Switch](/gen2/ComponentsAndServices/Switch#mqtt-control) MQTT `status_update` command toggles switch state
* [Plus1PM Mini](/gen2/Devices/Gen2/ShellyPlus1PM), [PlusPM Mini](/gen2/Devices/Gen2/ShellyPlusPMMini) Improved resilience of BL0942 power meter driver
* [Scripting](/gen2/ComponentsAndServices/Script) Phantom script contents when invoking `Script.Delete` / `Script.Create`
* [Scripting](/gen2/ComponentsAndServices/Script) Optimize function parsing and garbage collection
* [Cover](/gen2/ComponentsAndServices/Cover) Improved calibration procedure
* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT) Fix applying offset of temperature and rh
* [Light](/gen2/ComponentsAndServices/Light) `brightness` argument in [`Light.Set`](/gen2/ComponentsAndServices/Light#lightset) is parsed incorrectly
* [Light](/gen2/ComponentsAndServices/Light) Fix behavior of `min_brightness_on_toggle`
* [Light](/gen2/ComponentsAndServices/Light) Invoking `Light.Set` with `transition_duration` sets brightness to 0%
* [Light](/gen2/ComponentsAndServices/Light) Button presets don't work in `dual_dim` mode
* [Light](/gen2/ComponentsAndServices/Light) HTTP endpoint `/light/id` does not perform toggle
* [Input](/gen2/ComponentsAndServices/Input) Fix input reading on boot
* [HTTP](/gen2/ComponentsAndServices/HTTP) Relax parsing HTTP response lines
* [WiFi](/gen2/ComponentsAndServices/WiFi) Randomize AP channel
* [Webhook](/gen2/ComponentsAndServices/Webhook) Optimize handling of loopback calls
* Fixed UAF in timers
* Fix error message when RPC rejects due to lockout
* Prevent re-scheduling of HW timers while process is pending
* Track min queue free for the main queue

### Local web ###

### Fixed ###

* Bluetooth settings for PlusHT throws an error on open
* The firmware table does not scale correctly on mobile phones
* The color scheme for PlusPlugS and PlusPlugUK does not update the color
* Input settings for the Plus Addon for Plus2PM in cover mode throws an error
* Action cannot be deleted when the URL is invalid
* Negative sunset/sunrise values are not displayed correctly

### Added ###

* Local web collects logs when open (not only at Diagnostics page)
* Added `connected` status for the cloud icon in the status bar
* Script examples and snippets caching mechanism
* Modbus support for ProXEM
* Full cron support for schedules
* Add MAC addresses for Ethernet, BLE and WiFi
* Advanced link for KVS and diagnostics
* Button to clear log cache from the diagnostics page

### Changed ###

* Debug log reconnecting strategy
* KVS manager improvements
* Firmware page UI
* Limit calls to schedule calls
* Countdown animation on auto on and auto off
* Script editor improvements
* Diagnostic and script console rework
* For single-component devices, skip component selection for actions

[1.0.6] 2023-10-09
----------

### Changed ###

* [Pro x EM] Introduce adaptive logic for emitting power meter updates
* [Pro x EM] Remove no-load condition

### Added ###

* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM), [ProEM](/gen2/Devices/Gen2/ShellyProEM): User button (marked as reset) can be used to toggle the add-on relay or the built in relay.

### Fixed ###

* [ProEM](/gen2/Devices/Gen2/ShellyProEM) Fix conditional webhooks.

[1.0.5] 2023-09-26
----------

This version was only released for the ProEM device.

### Fixed ###

* [ProEM](/gen2/Devices/Gen2/ShellyProEM) Energy values recorded are significantly lower

[1.0.3] 2023-09-12
----------

### Changed ###

* Disable safe mode

[1.0.2] 2023-09-11
----------

### Fixed ###

* [`MQTT`](/gen2/ComponentsAndServices/Mqtt) Fix connection when using TLS
* [`MQTT`](/gen2/ComponentsAndServices/Mqtt) Fix crashes caused by storing a freed queue entry
* [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Fix crash caused by memory leak
* [Debug logs](/gen2/General/DebugLogs) Fix password protection of `/debug/log`: accept regular HTTP auth as well as auth via query string
* [BLE](/gen2/ComponentsAndServices/BLE) Fix crash caused by incorrect connection close
* [`Cover`](/gen2/ComponentsAndServices/Cover#http-endpoint-rollerid) HTTP Endpoint `/roller/id`: fix parsing of `offset` and `duration`
* [`Cover`](/gen2/ComponentsAndServices/Cover) Fix behavior of one-button mode after reboot / power-cycle
* [`Cover`](/gen2/ComponentsAndServices/Cover) Fix support of interlocking switches
* Optimize network buffer usage
* HTTP auth: Fix URI when computing digest response (include query string, if present)
* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT), [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) Drop [BLE observer](/gen2/ComponentsAndServices/BLE#configuration) option for battery operated devices

### Changed ###

* [`HTTP`](/gen2/ComponentsAndServices/HTTP#httprequest) `HTTP.Request`: adjust limitations on request headers
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Increase report interval

### Local web ###

### Fixed ###

* Idle power threshold setting for Cover now accept float values
* Bluetooth RPC and cloud gateway can be enabled only if the main Bluetooth is enabled
* Idle confirm period setting for Cover now have proper validation
* Movement time limit setting for Cover now have proper validation
* Added missing `Pause` action for Cover safety switch
* Added missing `Led indication` setting for PlusWallDimmer
* Show correct name for component when creating local action

* Remove Bluetooth observer option for battery operated devices
* Fix description of Bluetooth settings for battery-operated devices
* Sometimes the snackbar shows `undefined`
* Cannot set "LED indication mode" for `PlusPlugS`
* Clear script `updating` status at the start
* Fix placeholder when no scripts are available

### Changed ###

* Firmware update page improvements
* Improved dialog for creating schedules
* Auto OFF and ON timers now support float values

### Added ###

* Show network frequency for EM, EM1 and Switch components (only PM devices)
* Action on power ON for PlusWallDimmer
* Ability to upload firmware from .zip file
* Show banner when the device boots in `safe mode`

[1.0.1] 2023-08-24
----------

### Fixed ###

* [Plus1PM Mini](/gen2/Devices/Gen2/ShellyPlus1PM), [PlusPM Mini](/gen2/Devices/Gen2/ShellyPlusPMMini) Incorrect energy accumulation

[1.0.0] 2023-08-03
----------

### Added ###

* [`EM`](/gen2/ComponentsAndServices/EM) [Modbus registers](/gen2/ComponentsAndServices/EM#modbus-registers) for total current, total active power and total apparent power
* [`Input`](/gen2/ComponentsAndServices/Input) `invert` and `range_map` [configuration](/gen2/ComponentsAndServices/Input#configuration) properties for `analog` input type
* [`Light`](/gen2/ComponentsAndServices/Light) `min_brightness_on_toggle` [configuration](/gen2/ComponentsAndServices/Light#configuration) property
* [`Light`](/gen2/ComponentsAndServices/Light) HTTP Endpoint [`/light/{id}`](/gen2/ComponentsAndServices/Light#http-endpoint-lightid)
* Authentication in HTTP client, supporting basic and digest schemes. This enables the [HTTP](/gen2/ComponentsAndServices/HTTP) service and [webhooks](/gen2/ComponentsAndServices/Webhook) to access password-protected URLs.
* Support for `Pro3EM` [Addon](/gen2/Addons/ShellyProOutputAddon)
* Introduced a [15kB limit on script size](/gen2/Scripts/ShellyScriptLanguageFeatures#resource-limits)
* `Date` support in [scripting](/gen2/Scripts/ShellyScriptLanguageFeatures)
* Inbound HTTP RPC channel: [New query string syntax](/gen2/General/RPCChannels#get-with-query-string) which allows setting nested JSON properties by path, e.g. `/rpc/Sys.SetConfig?config.device.name=Some Name`
* [`Cover`](/gen2/ComponentsAndServices/Cover) `last_direction` attribute in [status](/gen2/ComponentsAndServices/Cover#status)
* `btoh` function added in [scripting](/gen2/Scripts/ShellyScriptLanguageFeatures#btoh)
* [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Add option to reverse CT direction of measurement for active power and energy
* Add network frequency in status of `EM`, `Switch`, `Cover` components. *shown if applicable*

### Changed ###

* [`Shelly.CheckForUpdate`](/gen2/ComponentsAndServices/Shelly#shellycheckforupdate) now returns an error instead of an empty result when device was unable to query the server.
* Restrict access to [log streams over websocket](/gen2/General/DebugLogs#logs-over-websocket) when [authentication](/gen2/General/Authentication) is enabled
* [`Script.PutCode`] cannot overwrite a running script. An error is returned if the script is running.
* [`Light`](/gen2/ComponentsAndServices/Light) deprecate `default.brightness` property in [Light configuration](/gen2/ComponentsAndServices/Light#configuration)
* [`Cover`](/gen2/ComponentsAndServices/Cover) bump max settable value of `motor.idle_confirm_period` [configuration](/gen2/ComponentsAndServices/Cover#configuration) to 2s
* WiFi: drop support for TKIP in AP mode. TKIP is a weak legacy cypher.
* BLE Scanner de-duplicates identical scan results within a 3-second window.

### Removed ###

* [`Sys`](/gen2/ComponentsAndServices/Sys) Drop `wakeup_period` attribute from [configuration](/gen2/ComponentsAndServices/Sys#configuration) (deprecated since 0.11.0)
* [`Webhook`](/gen2/ComponentsAndServices/Webhook) Drop `hook_types` object from [`Webhook.ListSupported`](/gen2/ComponentsAndServices/Webhook#webhooklistsupported) response (deprecated since 0.11.0)
* Timezone aliases and historical definitions listed in IANA's [`backward`](https://github.com/eggert/tz/blob/main/backward) file.

### Fixed ###

* [Plus2PM](/gen2/Devices/Gen2/ShellyPlus2PM) Configuration of [sensor addon](/gen2/Addons/ShellySensorAddon) components is reset on profile change

### Local web ###

### Added ###

* Display device time in local web footer
* New settings for switches - "External consumption type"
* Cover: Add position hint information when creating schedule for position
* Support for `Pro3EM` [Addon](/gen2/Addons/ShellyProOutputAddon)
* Wi-Fi roaming setting in Wi-Fi settings page
* New page Global Schedules - show every created schedule per component
* New page Global Actions - show every created action per component
* Scripting: Shortcuts for save and run
* Scripting: States such as Updating, Saved, Stopped, Running no longer use pop-up messages but unified UI state

### Fixed ###

* Pro2PM: Schedule Type error after ota update
* Cover: When creating action to execute "when open" it is showed as "opening"
* Adding scripts from library glitches in Firefox
* Pro3EM: Download csv timestamps were not dynamic
* Cover: Schedule with "undefined" position could be created
* Scripts were not updated when deleting
* Schedules: Action was showing "undefined" if the method is saved with upper case letter
* Schedules: PlusI4, Pro3EM empty component

### Changed ###

* Script editor improvements
* New UI and UX of the schedules
* Device reboot and device reset are now quick buttons in Settings list
* Scripting: Improved visuals

[0.14.4] 2023-05-10
----------

### Fixed ###

* [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Update default max power and max current limits

[0.14.3] 2023-04-20
----------

### Fixed ###

* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) OTA update via cloud

### Added ###

* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) New hook type [`smoke.alarm_off`](/gen2/ComponentsAndServices/Smoke#webhook-events)

[0.14.2] 2023-03-28
----------

### Fixed ###

* [PlusWallDimmer](/gen2/Devices/Gen2/ShellyPlusWallDimmer) Restore night mode in case of power loss
* [PlusWallDimmer](/gen2/Devices/Gen2/ShellyPlusWallDimmer) Looped trigger of [`light.on` / `light.off` webhooks](/gen2/ComponentsAndServices/Light#webhook-events)

### Local Embedded Web ###

* Improvement: PlusWallDimmer - Minor improvement on summary cards UI
* Bug fix: PlusWallDimmer, improve auto on/off timers animation

[0.14.1] 2023-03-08
----------

### Fixed ###

* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT) [`Temperature`](/gen2/ComponentsAndServices/Temperature) and [`Humidity`](/gen2/ComponentsAndServices/Humidity) offsets are applied by twofold
* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) Disable `active_between` property in [`Webhooks`](/gen2/ComponentsAndServices/Webhook)

### Changed ###

* Relax notifications rate limit for the [`Input`](/gen2/ComponentsAndServices/Input#rate-limit-for-notifications) component (80 notifications for a period of 60 seconds)
* [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Update max power and max current limits

### Local Embedded Web ###

* Use `zopfli` to compress the Web UI bundle
* Minor bug fix of behavior for attached/detached inputs

[0.14.0] 2023-02-28
----------

### Added ###

* [`EM`](/gen2/ComponentsAndServices/EM) Ability to calibrate a new CT from an existing one, [`EM.PhaseToPhaseCalib`](/gen2/ComponentsAndServices/EM#emphasetophasecalib) and [`EM.PhaseToPhaseCalibReset`](/gen2/ComponentsAndServices/EM#emphasetophasecalibreset)
* [`EM`](/gen2/ComponentsAndServices/EM) Add `no_load` error
* Notifications rate limit for the [`Input`](/gen2/ComponentsAndServices/Input#rate-limit-for-notifications) component
* [`MQTT Control`](/gen2/ComponentsAndServices/Mqtt#mqtt-control) Additional topics which allow commands to be sent to the device as well as for publishing results
* [`BLE`](/gen2/ComponentsAndServices/BLE#observer) Bluetooth observer

### Fixed ###

* [`HTTP.Request`](/gen2/ComponentsAndServices/HTTP#httprequest) cannot perform POST HTTPS request to specific sites

### Changed ###

* [Pro4PM](/gen2/Devices/Gen2/ShellyPro4PM) Show channel name on display when set, if it contains latin characters only.

### Local Embedded Web ###

* New feature: Add support for MQTT control
* New feature: Add support for RPC over MQTT
* New feature: Add support for bluetooth gateway
* New feature: Add phase to phase calibration for Pro3EM
* Improvement: Improve the diagram view for Pro3EM

[0.13.2] 2023-02-21
----------

### Fixed ###

* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT) Implement a full refresh every 24h (at night time) to clear any artefacts on ePaper display
* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT) Improve display update temperature threshold (change to 0.2C)

[0.13.1] 2023-02-09
----------

### Local Embedded Web ###

* Bug fix: [Pro3EM](/gen2/Devices/Gen2/ShellyPro3EM) Totals of active power, apparent power, current are `null`

[0.13.0] 2023-02-09
----------

### Added ###

* [`Switch`](/gen2/ComponentsAndServices/Switch), [`Cover`](/gen2/ComponentsAndServices/Cover) Undervoltage protection
* [`Switch`](/gen2/ComponentsAndServices/Switch) Automatic recovery from overvoltage/undervoltage errors
* [`Input`](/gen2/ComponentsAndServices/Input) Triple push notification and webhook
* [`EMData`](/gen2/ComponentsAndServices/EMData) Perpetual total energy counters
* [`EM`](/gen2/ComponentsAndServices/EM) `total_current`, `total_act_power`, `total_aprt_power` attributes in status

### Fixed ###

* [`Switch`](/gen2/ComponentsAndServices/Switch) Improve power measurement for `Plus1PM`, `PlugUS`, `PlusPlugS`, `PlusPlugIT`, `PlusPlugUK` (fixes erroneous overvoltage errors; fixes parasitic energy reports when no load is connected)
* [`Switch`](/gen2/ComponentsAndServices/Switch) Optimize power measurement notifications
* [`Switch`](/gen2/ComponentsAndServices/Switch), [`Cover`](/gen2/ComponentsAndServices/Cover) Reduce aggressiveness of overpower/overcurrent protection
* [`Switch`](/gen2/ComponentsAndServices/Switch), [`Cover`](/gen2/ComponentsAndServices/Cover) Parasitic status change notifications on overvoltage, overpower and overcurrent errors
* [`Switch`](/gen2/ComponentsAndServices/Switch), [`Light`](/gen2/ComponentsAndServices/Light), [`WiFi`](/gen2/ComponentsAndServices/WiFi) Inaccurate `*.SetConfig` error messages
* [`Webhook`](/gen2/ComponentsAndServices/Webhook) `active_between` is interpreted incorrectly when period spawns across the next day
* [`Script`](/gen2/ComponentsAndServices/Script) Crashes when specific scripts are enabled to start on boot
* [`EMData`](/gen2/ComponentsAndServices/EMData) CSV data download HTTP params processing
* [`EMData`](/gen2/ComponentsAndServices/EMData) Missing MODBUS data for energy on phases B and C
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Support dynamic LED transition ranges based on power limit settings
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK), [PlusPlugIT](/gen2/Devices/Gen2/ShellyPlusPlugIT) Update max power limit to match device prints
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Improve reaction time of LEDs in power mode
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Wrong brightness of network status indication
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS), [PlusPlugUK](/gen2/Devices/Gen2/ShellyPlusPlugUK) Restore night mode in case of power loss
* [PlusPlugS](/gen2/Devices/Gen2/ShellyPlusPlugS) Ambiguous voltage shown when output is off
* [PlugUS](/gen2/Devices/Gen2/ShellyPlugUS), [PlusPlugIT](/gen2/Devices/Gen2/ShellyPlusPlugIT) Wrong LED indication after factory reset
* [Plus2PM](/gen2/Devices/Gen2/ShellyPlus2PM), [Pro2PM](/gen2/Devices/Gen2/ShellyPro2PM) Guarantee outputs don't turn on after factory reset from `cover` to `switch` profile
* [Pro4PM](/gen2/Devices/Gen2/ShellyPro4PM) Display shows wrong time when not synced with NTP
* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) Battery charge is not displayed
* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) Missing `id` in status change notifications
* [PlusSmoke](/gen2/Devices/Gen2/ShellyPlusSmoke) Does not factory reset with 5 button clicks from config mode

### Local Embedded Web ###

* New device support: Added support for Plus Plug S
* New device support: Added support for Plus Plug IT
* New device support: Added support for Plus Plug UK
* New device support: Added support for Pro 3EM
* New feature: Added build version for local web UI
* New feature: Detect firmware update and show message asking for a refresh of the page
* New feature: Add `Undervoltage protection` setting for devices with power metering
* New feature: Add settings for auto recovery for Over/under voltage
* New feature: Add RPC over UDP
* New feature: Add Actions: Webhook-Event for triplepush
* New feature: Add tripplepush input visualisation
* New feature: Add Pro3EM error handling visualisation
* New feature: Add support for Pro3EM actions
* Improvement: Create placeholder with prompt when no scripts
* Improvement: Saving script causes errors in some weird situations
* Improvement: IP and network mask are the only required settings for static IP
* Improvement: Add cover profile default route to home -\> /cover/0/overview
* Improvement: Set `Action on power on` default value to `off` when is required
* Bug fix: Ensure `Units` settings is only visible on devices which have units
* Bug fix: Plus Addon - Non-blocking TypeError when adding peripheral
* Bug fix: `RangeError: Invalid time value` error when a device had issues with syncing time
* Bug fix: Can't configure Outbound Web Socket with `TLS no verification` and a `wss://` link on version 0.12.0
* Bug fix: Fix the disappearing factory reset by input checkbox
* Bug fix: Fix showing incorrect component when changing index in URL
* Bug fix: Submenu's active bar is not correctly displayed
* Bug fix: Home is side navigation is not highlighted
* Bug fix: Empty actions placeholder contains wrong icon
* Bug fix: Fix incorrect Pro3EM sum of totals
* Bug fix: Fix timer freezing
* Minor: Home page URL handling for Plus/Pro2PM (Cover/Switch)
* Minor: Actions - Slider text improvement

[0.12.0] 2022-12-06
----------

### Added ###

* [Sensor Add-On](/gen2/Addons/ShellySensorAddon) support for `Plus1`, `Plus1PM`, `Plus2PM`, `PlusI4`, `PlusI4DC`
* [`Voltmeter`](/gen2/ComponentsAndServices/Voltmeter) component
* [`Input`](/gen2/ComponentsAndServices/Input) component: support digital and analog inputs
* Webhook: new types [`input.analog_change`](/gen2/ComponentsAndServices/Input), [`input.analog_measurement`](/gen2/ComponentsAndServices/Input), [`voltmeter.measurement`](/gen2/ComponentsAndServices/Voltmeter), [`temperature.measurement`](/gen2/ComponentsAndServices/Temperature), [`humidity.measurement`](/gen2/ComponentsAndServices/Humidity)
* [Scripts](/gen2/Scripts/ShellyScriptLanguageFeatures): Base64 encoding and decoding
* [Scripts](/gen2/Scripts/ShellyScriptLanguageFeatures): Access bluetooth functionality - device discovery
* Embedded web: new device UI. Add "Actions" - control local device functionality on component events

### Fixed ###

* [Cover](/gen2/ComponentsAndServices/Cover): `Cover.SetConfig` error messages when arguments are out of range
* [Cover](/gen2/ComponentsAndServices/Cover): calibration fails when `obstruction_detection.holdoff` exceeds open/close duration
* ECO Mode fails to apply after WiFi reconnect
* [Webhook](/gen2/ComponentsAndServices/Webhook): fix invocation of `http://localhost` / `http://127.0.0.1` urls
* [Scripts](/gen2/Scripts/ShellyScriptLanguageFeatures): fix memory leak in `Shelly.emitEvent`
* [`Light`](/gen2/ComponentsAndServices/Light) component: fix validation of [`night_mode.active_between`](/gen2/ComponentsAndServices/Light#configuration) parameter

### Changed ###

* [PlusHT](/gen2/Devices/Gen2/ShellyPlusHT): Change [`wakeup_period`](/gen2/ComponentsAndServices/Sys#status) to 2h

[0.11.4] 2022-10-24
----------

### Added ###

* Sys: Add event to announce scheduled soft restart
* Webhook: Add expanded context for evaluation of conditions and token replacement and configurable repeatability
* Temperature and Humidity: offset
* Cover: configurable idle hold-off period

### Changed ###

* BLE: Updated configuration to include separate `enable` flag for the RPC service
* Sys: `restart_required` property is no longer set to `true` when a restart is scheduled automatically
* RPC handlers are disabled when a soft reboot is scheduled. Error code will be -109
* Webhook: Expand the context for evaluation of conditions and token replacement with device status, configuration and info
* Cover: last position is stored in non-volatile memory when movement ends

### Fixed ###

* Duplicate notification for some types of events
* Cover: losing position when multiple GoToPosition commands are enqueued
* Increased CPU frequency limit in ECO Mode
* PlusHT: fixes in display behavior
* Cover: improve stability with ECO Mode

[0.11.3] 2022-10-14
----------

### Fixed ###

* Device instability caused by ZX synchronizer during flash operations
* Memory leak in scripts

[0.11.2] 2022-10-04
----------

### Changed ###

* `Pro1PM`, `Pro2PM`, `Pro4PM`, `Plus2PM`: Synchronize output operations with voltage zero-cross

### Fixed ###

* Off-by-1 error in some timezones

[0.11.1] 2022-09-09
----------

### Fixed ###

* Mis-provisioned `Plus1`, `Plus1PM` devices

[0.11.0] 2022-08-30
----------

### Embedded/local web improvements: ###

* When editing a script, there is a “**Snippets**” section, which allows you to use snippets to write code faster
* On the Scripts (listing) page, there is a new **Library** button, that allows you to install scripts, directly from our GitHub page
* In the scripts library, you can change the library url for the specific device and **load your own library**

### API Documentation improvements: ###

* Major restructuring of the documentation, so that most of the APIs are now easy to find in the new combined “**Components and Services**” section
* Request, responses are now reformatted to look better/are easier to use/understand
* Formatting of parameters, error codes and others are now rendered in tables to improve readability
* Each Component/Service page is now following similar page structure
* New components and their respective documentation had been added (see next)

### Added ###

* [client\_id](/gen2/ComponentsAndServices/Mqtt#configuration) parameter in MQTT configuration
* [discoverable](/gen2/ComponentsAndServices/Sys#configuration) property to System configuration
* [Range extender](/gen2/ComponentsAndServices/WiFi#configuration)
* [Outbound Websocket](/gen2/ComponentsAndServices/Ws) component
* [Webhooks](/gen2/ComponentsAndServices/Webhook) and [schedules](/gen2/ComponentsAndServices/Schedule) revisions
* [Webhooks](/gen2/ComponentsAndServices/Webhook): conditions; variable interpolation in URLs
* Status change notification for [cfg\_rev](/gen2/ComponentsAndServices/Sys#status) attribute
* [KVS](/gen2/ComponentsAndServices/KVS) service
* [Temperature](/gen2/ComponentsAndServices/Temperature) component
* [Humidity](/gen2/ComponentsAndServices/Humidity) component
* [DevicePower](/gen2/ComponentsAndServices/DevicePower) component
* [Light](/gen2/ComponentsAndServices/Light) component
* [Sleep](/gen2/General/SleepManagementForBatteryDevices) management for battery-operated devices
* Scripts: register [handlers](/gen2/Scripts/ShellyScriptLanguageFeatures#http-handlers) to incoming HTTP requests
* Scripts: [broadcast events](/gen2/Scripts/ShellyScriptLanguageFeatures#shellyemitevent)
* Scripts: synchronous access to [configuration](/gen2/Scripts/ShellyScriptLanguageFeatures#shellygetcomponentconfig), [status](/gen2/Scripts/ShellyScriptLanguageFeatures#shellygetcomponentstatus), [device info](/gen2/Scripts/ShellyScriptLanguageFeatures#shellygetdeviceinfo), [current script id](/gen2/Scripts/ShellyScriptLanguageFeatures#shellygetcurrentscriptid)

### Changed ###

* MQTT: Change MQTT QOS level to 1
* MQTT: Retain LWT messages
* BLE: Require restart to apply BLE config changes
* Scripts: Error handling behavior changes to a more strict mode. Previously, errors during script execution only terminated the current context -- specific callback invokcation, for example. Now, errors encountered during script execution terminate the script and are reflected in its status.
* For battery-operated devices: deprecate `wakeup_period` property in [System configuration](/gen2/ComponentsAndServices/Sys#configuration) (moved to [System status](/gen2/ComponentsAndServices/Sys#status))

### Fixed ###

* Scripts: Script causing device crashes are detected and disabled automatically
* Scripts: Crash on MQTT unsubscribe when MQTT is disabled
* Power values oscillation between 0W and 1W on Plus1PM
* Crash when calling Shelly.Update without parameters
* Wrong aenergy values with low-power loads on Pro devices
* Validation of cid and event parameters of [Webhook.Create](/gen2/ComponentsAndServices/Webhook#Webhook.Update), [Webhook.Update](/gen2/ComponentsAndServices/Webhook#Webhook.Update)
* Crash due to race-conditions between TCP errors and queued callbacks
* Poor device responsiveness during HTTPS webhooks execution
* Incorrect ACL when authenticaion is disabled
* Erroneous overpower events on `Plus1PM` and `PlugUS` devices
* MQTT: Ignored [`topic_prefix`](/gen2/ComponentsAndServices/Mqtt#configuration)

[0.10.3] 2022-06-17
----------

### Fixed ###

* Erroneous overvoltage events on `Plus1PM` devices

[0.10.2] 2022-05-31
----------

### Fixed ###

* Wrong power consumption values displayed on Pro4PM boot
* Incorrect behavior of reset button (all devices)
* Fix mis-provisioned `Plus1PM` devices

[0.10.1] 2022-03-30
----------

### Fixed ###

* Schedules around DST time shifts

[0.10.0] 2022-03-08
----------

### Added ###

* New [HTTP.Request](/gen2/ComponentsAndServices/HTTP#httprequest) RPC method with support for `GET`, `POST`, `PUT`, `HEAD` and `DELETE`.
* [Cover](/gen2/ComponentsAndServices/Cover) component
* Only applicable for multi-profile devices: RPC methods [Shelly.ListProfiles](/gen2/ComponentsAndServices/Shelly#shellylistprofiles), [Shelly.SetProfile](/gen2/ComponentsAndServices/Shelly#shellysetprofile); `profile` key in the responses of [Sys.GetConfig](/gen2/ComponentsAndServices/Sys#configuration), [Shelly.GetDeviceInfo](/gen2/ComponentsAndServices/Shelly#shellygetdeviceinfo) and [/shelly](/gen2/ComponentsAndServices/Shelly#http-endpoint-shelly)
* Support for [`/ota` HTTP endpoint](/gen2/ComponentsAndServices/Shelly#http-endpoint-ota), for backward compatibility with Gen1 devices.
* Embedded web now has UI for changing the display brightness on Pro4PM
* Device name (if set) is now shown everywhere in the UI of embedded web to ensure users, using multiple browser tabs, would know on
  which device they are making their changes
* **Experimental support** for [Economy mode](/gen2/ComponentsAndServices/Sys) in the embedded web, decreasing power consumption of devices when latency is not critical.
  Since, this is still experimental, there is no support for changing it in the application yet.
  Enabling the option may have adverse effects and we do not recommend it for general usage. At this stage, it is intended for testing purposes and power consumption measurements.

### Changed ###

* Switch: setting `power_limit` to `null` will apply the default overpower threshold instead of disabling overpower protection.
* MQTT: do not show `pass` in response of `MQTT.GetConfig`
* Change response format of [Shelly.ListProfiles](/gen2/ComponentsAndServices/Shelly#shellylistprofiles)
* Improved Plus I4 UI in embedded web

### Fixed ###

* Scripts: Fixed Status change notifications being duplicated as Event notifications.
* Webhooks: fixed decoding of URLs containing the `"` character.
* Power factor measurement on Pro4PM.
* Initial/on start up power metering improvements
* `WiFi|Eth.SetConfig` - fixed ipv4mode invalid argument error message
* Ethernet improvements that should fix some issues with devices hanging/crashing
* Embedded web - Wrong channel name was displayed on Plus I4
* Disable SMP (Symmetric Multiprocessing) on all devices

[0.9.3] 2022-01-17
----------

### Fixed ###

* Broken `aenergy` update in `Switch` component [status](/gen2/ComponentsAndServices/Switch#status)

[0.9.2] 2022-01-14
----------

### Added ###

* **Experimental support** for [Economy mode](/gen2/ComponentsAndServices/Sys#configuration), decreasing power consumption of devices when latency is not critical. We do not include support for this feature in application and local web interface. Enabling the option may have adverse effects and we do not recommend it for general usage. At this stage, it is intended for testing purposes and power consumption measurements.
* Local web interface: Display the input state of the switch
* Local web interface: Explanation of power limit
* Ability to do OTA Update from url

### Changed ###

* [`Webhook.Update`](/gen2/ComponentsAndServices/Webhook#webhookupdate) can now modify `cid` (component instance id) of an existing webhook.

### Fixed ###

* Display negative values for `apower` and `aеnergy` in `Switch` component [status](/gen2/ComponentsAndServices/Switch#status)
* `ssl_ca` and `name` validation in Webhook.Update
* `unixtime` will be `null` in Sys.GetStatus when not synced with NTP server
* Ethernet IP address notification on connect
* Local web interface: Pro4PM issue with authentication menu
* Local web interface: Time in local webpage not correct

[0.9.1] 2021-12-03
----------

### Fixed ###

* Local web interface: Webhook, Script, Schedule list
* Local web interface: invert switch
* Local web interface: Input/Output-Setting & Invert Switch is missing

[0.9.0] 2021-12-01
----------

### Added ###

* [MQTT](/gen2/Scripts/ShellyScriptLanguageFeatures#mqtt) support in scripts
* [Limitations of the resources](/gen2/Scripts/ShellyScriptLanguageFeatures#limitations) used by a script
* Option to set brightness of the Pro4PM's screen when it is idle through a new [UI component](/gen2/Devices/Gen2/ShellyPro4PM#ui)
* Basic [MQTT tutorial](/gen2/ComponentsAndServices/Mqtt#MQTTSetup) in the docs
* [Placeholder notation](/gen2/) in the docs
* Math API for [scripts](/gen2/Scripts/ShellyScriptLanguageFeatures#math-api)
* Initial release of [Shelly Scripts](/gen2/Scripts/ShellyScriptLanguageFeatures)
* User-configurable overvoltage (`voltage_limit`) and overcurrent (`current_limit`) protection in [Switch](/gen2/ComponentsAndServices/Switch#configuration)
* Local web interface: selection of discovered WiFi APs
* Configuration revision number added to [System Component](/gen2/ComponentsAndServices/Sys) configuration
* Set `active_between` parameter in Webhook.Create/Update with HH and MM, which are hours and minutes respectively, and can be specified with or without leading zeros in 24-hour format
* `device.name` parameter in [System Component](/gen2/ComponentsAndServices/Sys) configuration
* `sntp.server` parameter in [System Component](/gen2/ComponentsAndServices/Sys) configuration
* Limit maximum number of simultaneous non-persistent RPC channels

### Fixed ###

* Event and status handlers in scripts
* Plus1 crash when `Switch.SetConfig()` is invoked
* MQTT topic prefix configuration shows the correct default value
* Local web interface: schedules time set, Pro4PM channel handling

### Changed ###

* Overpower protection (`power_limit`) in [Switch](/gen2/ComponentsAndServices/Switch#configuration)can be disabled
* The response type of [`Webhook`](/gen2/ComponentsAndServices/Webhook): `Update`, `Delete`, `DeleteAll`; and [`Schedule`](/gen2/ComponentsAndServices/Schedule): `Update` and `Delete` methods is now empty (`null`), in unison with other APIs.

[0.8.1] - 2021-09-21
----------

### Added ###

* Firmware version and device temperature in the screen UI of Pro4PM
* RPC communication [over UDP](/gen2/General/RPCChannels#udp)

### Fixed ###

* [`/shelly` HTTP endpoint](/gen2/ComponentsAndServices/Shelly#http-endpoint-shelly) does not require authentication anymore
* Bug causing Pro4PM's screen to crash when scrolling too fast in one direction

[0.8.0] - 2021-09-13
----------

### Added ###

* Ability to [change the prefix](/gen2/ComponentsAndServices/Mqtt#configuration) of MQTT topics
* Ability to publish each component's status on a dedicated [MQTT topic](/gen2/ComponentsAndServices/Mqtt#configuration) `status/<component:[id]>`
* [Debug log streams](/gen2/General/DebugLogs) over UDP, MQTT and websocket
* New property `nameserver` in the [configuration](/gen2/ComponentsAndServices/Eth#configuration) of the Ethernet component
* Missing [timezones](/gen2/ComponentsAndServices/Shelly#shellylisttimezones)
* New method [HTTP.POST](/gen2/ComponentsAndServices/HTTP#httppost)
* HTTP `headers` and `body` in the response of [HTTP.GET](/gen2/ComponentsAndServices/HTTP#httpget)
* Changelog page :)

### Removed ###

* [Authentication over UART and MQTT](/gen2/ComponentsAndServices/Shelly#shellysetauth)

### Fixed ###

* Sporadic temperature jumps in the readings of temperature sensors
* Voltage reported as 0 when [Switch](/gen2/ComponentsAndServices/Switch#status) output is off

### Changed ###

* Streamline payloads of [event notifications](/gen2/General/Notifications#notifyevent): improve event descriptions, add reference to event origin

[0.7.0] - 2021-09-01
----------

### Added ###

* First public version released

[Previous Zigbee Features by Device](/gen2/Integrations/Zigbee/DeviceFeatures)
