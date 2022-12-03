# ESPHome Temperature and Humidity with OLED Display
Software and casing for a small device that works with ESPHome / Home Assistant to capture temperature and hudity and
display it locally. Includes a button to toggle screen saver / lights out mode.

![ESPHome Temperature Humidity OLED fully built](https://brett.durrett.net/wp-content/uploads/2022/12/full_build.jpeg)

## Software Setup

This setup assumed you are using [ESPHome](https://esphome.io/) through [Home Assistant](https://www.home-assistant.io/). If you are using ESPHome directly, the directions are likley _close enough_.

- [ ] From the ESPHome web interface in Home Assistant, select "+ New Device" (the green button in the lower right corner)
- [ ] From the "New device" dialog, you will be asked to select the first-time install method, "OPEN ESPHOME WEB" or "CONTINUE", these directions assume you continue via Home Assistant.
- [ ] In the "Create configuration" dialog, provide a name for this device
- [ ] In the "Select your device type", select the board you are using (we assume ESP8266, others may work)
- [ ] You should see a "Configuration created!" dialog, with the options to "SKIP", or "INSTALL". Select "SKIP"
- [ ] In the ESPHome web interface, find your device and select "EDIT". You should see pre-existing content that looks something like this:

```
esphome:
  name: tho-tutorial

esp8266:
  board: esp01_1m

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "[random chracters that are your key]"

ota:
  password: "[random characters that are your password]"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "THO Fallback Hotspot"
    password: "5EKR17"

captive_portal:
```    

- [ ] Append the following to the file

```
substitutions:
  friendly_name: "THO Tutorial"
  area_name: "Garage"

packages:
  bdurrett.esphome-temp-humid-OLED: github://bdurrett/esphome-temp-humid-OLED/temp-humid-OLED.yaml

```
- [ ] In the `esphome` section of your config, add an entry `name_add_mac_suffix: true` if you want the MAC address added to each device name (generally for bulk installs)
- [ ] In the `esp8266` section, comment out the board if it is not `d1_mini` (if you see errors about references to D6, D5, D1, or D2, this is the board not recognizing NodeMCU pins.

## Hardware Setup

FIXME TODO: Maybe add a narrative (that said, diagram is self explanatory)

### Parts
* ESP8266 board, any should work, [the ESP-12F is nice and tiny](https://smile.amazon.com/gp/product/B081PX9YFV/ref=ppx_yo_dt_b_asin_title_o01_s01?ie=UTF8&psc=1) and fits the 3D printed case
* SSD1306 OLED display, other types may work, I used [this one](https://smile.amazon.com/gp/product/B09C5K91H7/ref=ppx_yo_dt_b_asin_title_o01_s02?ie=UTF8&psc=1)
* 6mm button (momentary switch), I used [these](https://www.amazon.com/gp/product/B07C7211PJ/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1)
* A 10 K ohm resistor (for pull down)

### Wiring Diagram

![ESPHome Temperature Humidity OLED wiring diagram](https://brett.durrett.net/wp-content/uploads/2022/12/wiring-diagram.png)

Wiring diagram created with [Fritzing](https://fritzing.org/)

### Sorta Fancy (okay, Janky) Case
I finally got around to tuning up my 3D printer and making a model. The case can be a bit tight... I'm using 30 gauge wire, anything much thicker might be a beast to work with. The button used is 6x6mm, the OLED matches the one linked, above.

![Case](https://brett.durrett.net/wp-content/uploads/2022/12/build-01-scaled.jpeg)

## To Do
- [ ] Temperature (and humidity) seems higher, possibly heat from components influencing the ratings? Add configurable offsets to calibrate once good readings are known.
- [ ] Preceed the sensor labels with the friendly name


