# Nixie Display Demo

This Nixie Display Demo is a [Node-RED][nodered] Flow for the [Raspberry Pi][raspberrypi] and [Cathode Creations][cathodecreations] IN-8-2 Nixie board that demonsrates how to control the displays as well the LED illumination.

- Demonstrates how inject nodes can be used to update the entire display or to step individual digits in from the left.
- Provides an example of how to write to the LEDs.
- Also demonstrates how to blink the entire display or LEDs without changing the loaded values.

# Required Equipment

### Nixie Display

Each Cathode Creations [IN-8-2 Nixie Raspberry Pi board][nixie-board] display controls six single-digit nixie tubes. Unlike many simular looking products, this is not a clock, although it could certainly be used as one. Instead, it is a true arbitrary numeric display. Additionally, each tube can be individually illuminated. The $55 kit includes the PCB and the seperate components. Additionally, users will have to buy they own tubes (I found some on ebay delivered for about $10 each) and a 12v 2A power supply.

### Raspberry Pi

A [Raspberry Pi][raspberrypi] is also required. I have used both an origional Raspberry Pi Model B and a Raspberry Pi 2 Model B. Because of the simple hardware requirement, I anticipate that many other models will work as well, as long as they at least offer the original 26 GPIO pins.

Additionally, all the normal Raspberry Pi accessories (SD card, 5Vdc supply) will be needed. I strongly encourage the use of a case, since the Nixie PC board will have high voltages present.

# Software Setup

The ultimate goal of the following is to end up with a [Raspberry Pi][raspberrypi] running [Node-RED][nodered]. The following outlines the process I used to setup the software for my display. There are many ways to accomplish this, and many users may have a Raspberry Pi already setup and ready to go. For those who might not, or want a quick start guide, this shoudl get you there.

### Setup Raspbian Jessie Lite

1) Download the latest [Raspbian Jessie Lite][raspbian-jessie-lite]. The non-lite version can be used as well, if you have the need to use a display. Personally, the thought of have to use a video cable on this doesn't really fit the Nixie aesthetic.
2) Write the image to an SD card. This process is well documented elsewhere, here are some examples for [MAC][setup-mac] and [PC][setup-pc].

### Setup Node-RED

The previous step shows how to open a terminal shell into the Raspberry Pi. Continuing in that shell, the following instructions will get Node-RED started.

Depending on the path that lead to this point, it is possible Node-RED is aleady installed. Running the following command is a simple way to find out:
```sh
node-red-stop && node-red-start
```
If a message indicating `Start Node-RED` appears, then Node-RED is already installed and the rest of this section can be skipped. However if a message indicating `command not found` appears, then Node-RED will have to be installed. The following instructions outline one way to accomplish that.

Instructions appropriate for a Raspberry Pi are found on the [Node-RED Rapsberry Pi][nodered-raspberrypi] getting started guide. In many cases, it just boils down to pasting this block of text in to a terminal window.

```sh
node-red-stop && \
sudo apt-get update && \
sudo apt-get install nodered && \
node-red-start
```

### Opening Node-RED

Once everything is assembled and Node-RED is running, you should be able to open it from a web browser. For a default installation, that will be `http://<raspberry-pi-IP-address>:1880/`. If that doesn't work, check that you have entered the correct IP address for the Raspberry PI. Also, inspect the `setting.js` file and locate the `uiPort` entery. Either of the following commands should help.
```sh
cat /home/pi/.node-red/settings.js | grep uiPort
```
or
```sh
sudo nano /home/pi/.node-red/settings.js
```
### Using nixie-display-demo in Node-RED

With Node-RED open and an empty Flow tab visible, select the hamburger button in the upper right to open the menu. From the menu, select Import > Clipboard. Open the `nixie-display-demo.json` file, then select and copy it's contents. Return to Node-RED, paste the text and select Ok. Once the new Flow appeasr under the mouse, move it towards the upper left corner and click once. Select Deploy.

Power on the Nixie display. Use any of the blue injectors on the left side to send the indicated payloads. Note that none displayable characters (such as `a`, `z` and `_` in the example) will appear as turned off Nixie tubes.

Scroll down, and you will find a simular set of injectors for the LEDs.

### Notes

Before saving the .json file, it was run through the excellent [JSONLint][jsonlint] tool. I have found doing so makes identifying changes from the respository significantly easier than raw Node-RED output.

### Version
1.0.0

### Tech

This project benifited from other projects:

* [Dillinger] - Made with "Dillinger, the Last Markdown Editor ever."
* [Cathode Creations][cathodecreations-gh] - Origional Python script for the Nixie Display.

[//]: # (http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [cathodecreations]: <http://cathodecreations.com/>
   [cathodecreations-gh]: <https://github.com/cathodecreations/raspberrypi-nixie>
   [dillinger]: <http://dillinger.io/>
   [dillinger-gh]: <https://github.com/joemccann/dillinger>
   [jsonlint]: <http://jsonlint.com/>
   [nixie-board]: <http://cathodecreations.com/index.php?route=product/product&product_id=72>
   [nodered]: <http://nodered.org/>
   [nodered-raspberrypi]: <http://nodered.org/docs/hardware/raspberrypi>
   [raspberrypi]: <https://www.raspberrypi.org/>
   [raspbian-jessie-lite]: <https://www.raspberrypi.org/downloads/raspbian/>
   [setup-mac]: <https://www.raspberrypi.org/forums/viewtopic.php?t=74176>
   [setup-pc]: <http://www.circuitbasics.com/raspberry-pi-basics-setup-without-monitor-keyboard-headless-mode/>
