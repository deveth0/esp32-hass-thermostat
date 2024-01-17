# esp32-hass-thermostat

ESP32 based wifi Thermostat for Homeassistant.

Currently there are three hardware versions available:
* 1.54'' Display without buttons
* 1.54'' Display with buttons
* 2.9'' Display with buttons

All versions share a ESP32 D1 Mini as Microcontroller and use Waveshare epaper displays. 

## Gallery

<img src="https://i.imgur.com/9NtTPL2.jpg" width="400">
<img src="https://i.imgur.com/Qhs3QL5.jpg" width="400">
<img src="https://i.imgur.com/5rEku5x.jpg" width="400">
<img src="https://i.imgur.com/GKYN9dG.jpg" width="400">



## Hardware

### Controller and Buttons

The controller is a simple D1 Mini with ESP32 chip which supports Wifi and provides plenty of GPIO pins for this project.

I soldered three tactile buttons onto a PCB which I cut down to 30mm x 13mm so they fit into the case.

### Display
Pick one of the epaper displays from Waveshare:
* [1.54''- 200x200 px](https://www.waveshare.com/1.54inch-e-paper-module.htm)
* [2.9'' - 296x128 px](https://www.waveshare.com/2.9inch-e-paper-module.htm)

Although there are three color versions of the 2.9'' display available, those are not supported.

Note: Currently partial refreshes are only available for the 2.9'' display which therefor feels way more responsive

### Case

You can find `stl` files (and the FreeCad Sources) for several cases in this repository.

* `Thermostat_Case_1.54_Front.stl` and `Thermostat_Case_1.54_Back.stl`- Case for 1.54'' display without buttons
* `Thermostat_Case_1.54-Buttons_Front.stl` and `Thermostat_Case_1.54-Buttons_Back.stl`- Case for 1.54'' display with buttons
* `Thermostat_Case_2.9_Front.stl` and `Thermostat_Case_2.9_Back.stl`- Case for 2.9'' display with buttons and USB left
* `Thermostat_Case_2.9-right_Front.stl` and `Thermostat_Case_2.9-right_Back.stl`- Case for 2.9'' display with buttons and USB right

Note: the 2.9'' display has quite small mounting holes, the pins of the case break quite easily.

There are also some buttons you can print for the cases (they look way nicer when using a resin printer). 

## Setup

### Hardware

Solder the display and buttons to your D1 Mini. The displays need 3.3V. 

| GPIO | Usage |
|------|-------|
| GPIO21 | Display - CS | 
| GPIO22 | Display - MOSI / DIN| 
| GPIO25 | Display - BUSY| 
| GPIO26 | Display - RESET| 
| GPIO27 | Display - DC| 
| GPIO32 | Display - CLK | 

Measure the direction your tactile buttons switch and connect one side to GND and the other to the following pins (do this for all three buttons):

| GPIO | Usage |
|------|-------|
| GPIO18 | Button - Down | 
| GPIO19 | Button - Up | 
| GPIO23 | Button - Push | 

### Software

Install [esphome](https://esphome.io/) on your system and make sure it works. 

Create a `secrets.yaml` file with your wifi credentials:

```
wifi_ssid: "FOO BAR"
wifi_password: "12345678"
```

Pick the `yaml` file depending on the display and buttons, update the entity ids to reflect your Homeassistant setup and install it to the ESP32:

Example: 

`esphome run .\thermostat_2.9-right.yaml` 

