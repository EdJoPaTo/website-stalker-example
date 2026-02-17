Shelly 2.5
==========

Device identification
----------

* Device name: **Shelly 2.5**

* Device model: **SHSW-25**

* Device SSID: **shellyswitch25-XXXXXX**

Short description
----------

Shelly 2.5 is a small form factor 2-channel smart switch with power measurement and cover control, which allows remote control of electric appliances through a mobile phone, tablet, PC, or home automation system. It can work standalone in a local Wi-Fi network or it can also be operated through cloud home automation services.

Shelly 2.5 can be accessed, controlled and monitored remotely from any place where the User has internet connectivity, as long as the device is connected to a Wi-Fi router and the Internet.

It can be retrofitted into standard electrical wall boxes, behind power sockets and light switches or other places with limited space.

Shelly 2.5 has an embedded Web Interface which can be used to monitor and control the device, as well as adjust its settings.

Main applications
----------

* Residential

* MDU (Multi Dwelling Units - apartments, condominiums, hotels, etc.)

* Light commercial (small office buildings, small retail/restaurant/gas station, etc.)

* Government/municipal

* University/college

Integrations
----------

* Google

* Samsung SmartThings

* Alexa

Simplified internal schematics
----------

Device electrical interfaces
----------

### Inputs ###

* 2 switch/button input on screw terminal

* 3 power supply inputs on screw terminals: 1 N and 2 L

### Outputs ###

* 2 relay outputs with power measurement on screw terminal

### Add-on interface ###

* Shelly proprietary serial interface

**⚠CAUTION!** High voltage on the add-on interface when the Device is powered!

Connectivity
----------

* Wi-Fi

* Bluetooth (for inclusion purposes)

Safety features
----------

* Overheating protection

* Overpower protection

* Obstacle detection (cover mode)

* Safety switch (cover mode)

Supported load types
----------

* Resistive (incandescent bulbs, heating devices)

* Capacitive (capacitor banks, electronic equipment, motor start capacitors)

* Inductive with RC Snubber (LED light drivers, transformers, fans, refrigerators, air-conditioners)

User interface
----------

### Inputs ###

* One (Reset) button

  * Press and hold for 5 seconds to enable Device access point.

  * Press and hold for 10 seconds to factory reset the Device.

### Outputs ###

* LED (Red) indication

  * AP (Access Point) enabled and Wi-Fi disabled:
    1 second `ON` / ¼ second `OFF`

  * Wi-Fi enabled, but not connected to a Wi-Fi network:
    2 second `ON` / ¼ seconds `OFF`

  * Connected to a Wi-Fi network:
    Constantly `ON`

  * Cloud enabled, but not connected:
    1 second `ON` /5 seconds `OFF`

  * Connected to Shelly Cloud:
    Constantly `ON`

  * OTA (Over the Air Update):
    ½ sec `ON` / ½ second `OFF`

  * Button pressed and held for 5 seconds:
    ¼ second `ON` / ¼ second `OFF`

  * Button presses and held for 10 seconds:
    ⅛ second `ON` / ⅛ second `OFF`

The list above starts with the initial device status and the lowest priority. Every next state cancels the previous one.

Specifications
----------

|            Type            |                                          Value                                           |
|----------------------------|------------------------------------------------------------------------------------------|
|        **Physical**        |                                                                                          |
|       Size (HxWxD):        |                        36x39x17 ±0.5 mm / 1.42x1.54x0.67 ±0.02 in                        |
|          Weight:           |                                                                                          |
|         Mounting:          |                                       Wall console                                       |
|Screw terminals max torque: |                                    0.4 Nm / 3.5 lbin                                     |
|  Conductor cross section:  |                              0.5 to 1.5 mm² / 20 to 16 AWG                               |
| Conductor stripped length: |                               5 to 6 mm / 0.20 to 0.24 in                                |
|      Shell material:       |                                         Plastic                                          |
|           Color:           |                                          Black                                           |
|     **Environmental**      |                                                                                          |
|    Ambient temperature:    |                            \-20 °C to 40 °C / -5 °F to 105 °F                            |
|          Humidity          |                                     30 % to 70 % RH                                      |
|       Max. altitude        |                                     2000 m / 6562 ft                                     |
|       **Electrical**       |                                                                                          |
|       Power supply:        |                               110 - 240 VAC / 30 - 50 VDC                                |
|     Power consumption:     |                                          \< 1 W                                          |
|**Output circuits ratings** |                                                                                          |
| Max switching voltage AC:  |                                          240 V                                           |
| Max switching voltage DC:  |                                           50 V                                           |
| Max switching current AC:  |                             10 A (per channel), 20 A (total)                             |
| Max switching current DC:  |                             10 A (per channel), 20 A (total)                             |
|    **Sensors, meters**     |                                                                                          |
|Internal-temperature sensor:|                                           Yes                                            |
|       Wattmeter (AC)       |                                           Yes                                            |
|         **Radio**          |                                                                                          |
|          RF band:          |                                     2401 - 2495 MHz                                      |
|       Max. RF power:       |                                         \<20 dBm                                         |
|      Wi-Fi protocol:       |                                       802.11 b/g/n                                       |
|        Wi-Fi Range:        |Up to 30 m / 100 ft indoors and 50 m / 160 ft outdoors  <br/>(Depends on local conditions)|
|          **MCU**           |                                                                                          |
|            CPU:            |                                         ESP8266                                          |
|           Flash:           |                                           2 MB                                           |
| **Firmware capabilities**  |                                                                                          |
|         Schedules:         |                                            20                                            |
|  Webhooks (URL actions):   |                                 12 with 5 URLs per hook                                  |
|         Scripting:         |                                            No                                            |
|           MQTT:            |                                           Yes                                            |
|           CoAP:            |                                           Yes                                            |

Basic wiring diagram
----------

|   |   |   |
|---|---|---|

### Legend ###

|**Terminals**|                             |**Wires**|                         |
|-------------|-----------------------------|---------|-------------------------|
|    **N**    |      Neutral terminal       |  **N**  |      Neutral wire       |
|    **L**    |  Live (110-240 V) terminal  |  **L**  |Live (110 - 240 VAC) wire|
| **O1, O2**  |Load circuit output terminals|   \+    |30 - 50 VDC positive wire|
|**SW1, SW2** |   Switch input terminals    | **\-**  |30 - 50 VDC negative wire|

Troubleshooting
----------

...

Web Interface guide
----------

[Read the Shelly 2.5 web interface guide](https://kb.shelly.cloud/knowledge-base/shelly-2-5-web-interface-guide)

Components and APIs
----------

* [This device](https://shelly-api-docs.shelly.cloud/gen1/#shelly2-5)

* [All Shelly devices and services](https://shelly-api-docs.shelly.cloud/)

Printed User Guide
----------

[Download printed user guide - English, Deutsch, Italiano, Español, Português, Français](https://kb.shelly.cloud/__attachments/65994767/Download%20printed%20user%20guide%20-%20English,%20Deutsch,%20Italiano,%20Espa%C3%B1ol,%20Portugu%C3%AAs,%20Fran%C3%A7ais)

Compliance
----------

* [Shelly 2.5 multilingual EU declaration of conformity.pdf](https://kb.shelly.cloud/__attachments/266174494/Shelly%202.5%20multilingual%20EU%20declaration%20of%20conformity.pdf)

Installation guides
----------

Projects
----------

#### Home Automation: Roller Shutters, Lights, Scenes ####

A guide on how to configure and control your roller shutters and ambient of lights, connected to Shelly 2.5, using Amazon Alexa. If you also have a Shelly Door/Window sensor, you can learn how to define a scene to automatically control roller shutters or lights as a function of day time and main door status.

[Learn More](https://www.instructables.com/id/Home-Automation-Roller-Shutters-Lights-Scenes/)

#### Genius Natural Beer Cooler With Wow Effect Controlled With Shelly Smart Device ####

Create your very own natural beer cooler easily from drain pipes. The beer will be cooled underneath the earth and with an electrically driven motor it comes up if you want some. The genius beer cooler is controlled by a Shelly wifi switch which can be controlled via Siri or Alexa. Just say: “Siri (or Alexa) bring beer”.

[Learn More](https://www.instructables.com/id/Genius-Natural-Beer-Cooler-With-Wow-Effect-Control/)

Reviews
----------

#### We Smart ####

[Shelly 2.5 best way to install](https://www.youtube.com/watch?v=X96PoQ8H-dc)

#### Csongor Varga ####

[Shelly 2.5 – dual channel Wi-Fi relay with roller shutter mode](https://www.youtube.com/watch?v=DIPzbCsSaa4)

#### The Hook Up ####

[Does UL Listing Make Products Safer? Interview with Shelly about UL Certification of the Shelly 2.5](https://www.youtube.com/watch?v=92b26PI6Z3c)
