# Raspberry Pi Hardware
Instructions for how to equip a Raspberry Pi to control a JURA coffee maker.

## Examples:
<img src="https://user-images.githubusercontent.com/11741404/119830585-b608d400-befc-11eb-9a65-6c6e5319bb94.jpg" width="400"> <img src="https://user-images.githubusercontent.com/11741404/119830488-9a9dc900-befc-11eb-96ca-b56d4b393019.jpg" width="400">
<img src="https://user-images.githubusercontent.com/11741404/119830550-abe6d580-befc-11eb-8ba2-e2527019f66b.jpg" width="400"> <img src="https://user-images.githubusercontent.com/11741404/119830526-a38e9a80-befc-11eb-8cee-7ad982db629e.jpg" width="400">

## How it Works
![how_it_works](https://user-images.githubusercontent.com/11741404/119833706-9e7f1a80-beff-11eb-8dad-a5aeed06e33f.png)  
The Raspberry Pi (1) acts as the brain of the system.
It connects via UART to the coffee maker (2) and interacts with it.  
Also, the Raspberry Pi (1) is connected to a touchscreen display (2) allowing the user to interact with the coffee maker (2) in a simple way.
Besides that, the Raspberry Pi (1) supports optional authentication of uses, using their RFID/NFC cards.
To make this possible, the Raspberry Pi (1) is also connected to an RFID/NFC reader (4) via USB.
This reader sends the card IDs it reads as keyboard input to the Raspberry Pi (1).

## Hardware
In this section we have a look at the hardware required for this.
I used the following hardware for this project:
* [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)
* [SanDisk Extreme PRO R100/W90 microSDHC 32GB Kit, UHS-I U3, A1, Class 10 (SDSQXCG-032G-GN6MA)](https://geizhals.de/sandisk-extreme-pro-r100-w90-microsdhc-32gb-kit-sdsqxcg-032g-gn6ma-a1620851.html) - you need a fast one in case you want to debug on you Pi :)
* [Raspberry Pi Touch Display](https://www.raspberrypi.org/products/raspberry-pi-touch-display/)
* [NFC-Reader](https://www.amazon.de/gp/product/B07J2KWHKL/ref=ppx_yo_dt_b_asin_title_o06_s00?ie=UTF8&psc=1) - you can use anyone that sends the read card ID as follows "0123456789\n" as keyboard input
* [4-channel I2C-safe Bi-directional Logic Level Converter - BSS138](https://www.adafruit.com/product/757) - to covert the 5V signals from the coffee maker to 3.3V signals for the Pi
* Jumper cables for connecting everything up.

## 3D Printed Case
In the [3D-printer](3D-printer/README.cd) directory you can find more information about how to print a case for the Raspberry Pi, its display and attache it to the coffee maker.

## Software
In this section we have a look at the software required for this.

### Raspberry Pi OS
You need an up to date copy of [Raspberry Pi OS](https://www.raspberrypi.org/software/) or any other **Linux** distro running on your Rapsberry Pi.

### UI
For the UI we use the [gtk-ui](https://github.com/Jutta-Proto/gtk-ui). Head over there and have a look at the dependencies there.

## Connecting a Coffee Maker
TODO
