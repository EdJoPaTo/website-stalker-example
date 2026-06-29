On this Page
----------

Shelly RGBW2
==========

Downloads
----------

### Manuals  ###

[User and Safety Guide](https://kb.shelly.cloud/__attachments/a_535b07d2911c48ae8177cec6d89c769b433c9ca399ab15a5e2286a80f690940c/User%20and%20Safety%20Guide?cb=49f92c8fa7219c1d5bd40b020286d0e0)

[App Guide](https://kb.shelly.cloud/__attachments/a_913945c46f5ff5255547d6548fbe0fdf925dc19965d1cb795d946381bb547c69/App%20Guide?cb=a417d88864c1ac1874a56512cda9b73a)

[Wiring Diagrams](https://kb.shelly.cloud/__attachments/a_e83b1dd4ef15a1e05784c2d28b7a0563c7692d2bcdb348caa139128e4cc45186/Wiring%20Diagrams?cb=85202c7565d125839648e2c3f5c26316)

Compliance
----------

* [Shelly RGBW2 multilingual EU declaration of conformity.pdf](https://kb.shelly.cloud/__attachments/a_7df1d545392ab6dbc6adfc83b2bb760a8103aed631ef9e14c7dddc306dd707e3/Shelly%20RGBW2%20multilingual%20EU%20declaration%20of%20conformity.pdf)

* [Shelly RGBW2 UK PSTI ACT Statement of compliance.pdf](https://kb.shelly.cloud/__attachments/a_9ea505ea0b6de0508b31ef3c621c27b8686154fb3625eaeb59d861c087b86303/Shelly%20RGBW2%20UK%20PSTI%20ACT%20Statement%20of%20compliance.pdf?cb=050d1a0eb0712e236864122c6afec247)

* [Shelly RGBW2 x2 UK PSTI ACT Statement of compliance.pdf](https://kb.shelly.cloud/__attachments/a_b8eb48b846efea325a9f7cbb67c376d394c386236140c80acc0e9689d6563ff2/Shelly%20RGBW2%20x2%20UK%20PSTI%20ACT%20Statement%20of%20compliance.pdf?cb=c8b66b08deac0a3565369e47f7c279af)

What is Shelly RGBW2?
----------

#### WiFi-operated RGBW controller  ####

Make your LED strips smart in one easy step. Shelly RGBW2 can connect like any LED controller and allows you to control all your lighting directly from a mobile device or tablet.

#### Features  ####

* No HUB is required.

* Wide range of voltage support.

* Huge palette of different colors, dimming options, and effects.

* Designed to fit in most standard electrical boxes and switches.

* It can be integrated to work with all other Shelly devices.

* Compatible with Android, iOS, Amazon Alexa, Google Assistant, and home automation servers using MQTT, CoAP, and REST API.

* Easily make your Arduino project live and usable in your automation project.

|            **POWER**             |                                                                                |
|----------------------------------|--------------------------------------------------------------------------------|
|         Power supply AC          |                                       No                                       |
|         Power supply DC          |                                    12V/ 24V                                    |
| DC Power Output 12V per channel  |                                      45W                                       |
| DC Power Output 24V per channel  |                                      90W                                       |
|DC Power Output 12V combined power|                                      144W                                      |
|DC Power Output 24V combined power|                                      288W                                      |
|      **SPECIAL FUNCTIONS**       |                                                                                |
|  Device temperature protection   |                                       No                                       |
|       Overload protection        |                                       No                                       |
|        Power measurement         |                                      Yes                                       |
|             Dimming              |                                      Yes                                       |
|  Working without a neutral line  |                                       No                                       |
|           **FEATURES**           |                                                                                |
|         Colour changing          |                                      Yes                                       |
|        Predefined effects        |                                      Yes                                       |
|             Channels             |                                   4 Channel                                    |
|           Maximum load           |                                      12A                                       |
|     Operational temperature      |                                  0ºC to +40ºC                                  |
|     Device power consumption     |                                     \< 1 W                                     |
|        Intelligent On/Off        |                                      Yes                                       |
|     Local and remote control     |                                      Yes                                       |
|          Sunrise/Sunset          |                                      Yes                                       |
|         Weekly Schedule          |                                      Yes                                       |
|         UL Listed option         |                                       No                                       |
|         **CONNECTIVITY**         |                                                                                |
|      Wireless/WiFi Protocol      |                                  802.11 b/g/n                                  |
|          Radiofrequency          |                                2400 – 2500 MHz                                 |
|              Range               |up to 50 m outdoors and up to 30 m indoors (depending on the building materials)|
|          **DIMENSIONS**          |                                                                                |
|               Size               |                               43mm x 38mm x 14mm                               |

Wiring diagrams
----------

|   |   |
|---|---|

|   |   |
|---|---|

|   |   |
|---|---|

|   |   |
|---|---|

Use cases
----------

#### Universal lighting control  ####

Are you going to bed and need to switch off all the lights? Install Shelly RGBW2, and you will be able to control all lights with just one tap via your smartphone, or with your voice. It can manage RGB+W, 4x single-color LED strips, or the spotlights in your living room.

Projects
----------

#### MagicMirror With Gesture Controlled LED Strip Using Shelly RGBW2  ####

Learn how to create a MagicMirror of your own controlled by Shelly RGBW2 and LED strips on the front. Sounds cool, doesn’t it?

[Learn More](https://www.instructables.com/id/MagicMirror-With-Gesture-Controlled-LED-Strip-Usin/)

Reviews
----------

[Shelly RGBW2: A WiFi LED Controller with TONS of Options for $22](https://www.youtube.com/watch?v=B8DQntdtD4E)

 // Mark block images on the first level as breakout so they can grow wider than the article content. document.querySelectorAll('.article-body \> .theme-block-image [data-component="image"]').forEach((element) =\> { const propertyValue = element.style.getPropertyValue('--width'); if (!propertyValue) { return; } if (parseInt(propertyValue) \>= 760) { element.closest('.theme-block-image').classList.add('theme-block-image--breakout'); } }); // Remove the inline size on page layouts as this would lead to layouts breaking out of the article content. document.querySelectorAll('.article-body [data-component="layout-section"]').forEach((element) =\> { const propertyValue = element.style.getPropertyValue('--inline-size'); if (!propertyValue) { return; } // ONLY for this very specific width (Confluence default) if (parseInt(propertyValue) === 760) { element.style.removeProperty('--inline-size'); } }) // Set the initial state of the navigation toggle to prevent shifting in the UI try { const navigationToggle = document.querySelector('#navigator-toggle'); const navigationState = localStorage.getItem('theme-navigation-state'); if (navigationState === 'collapsed' && navigationToggle) { navigationToggle.setAttribute('aria-expanded', 'false'); } } catch (error) { console.error(error); }
