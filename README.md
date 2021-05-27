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


## Software
In this section we have a look at the software required for this.

### Raspberry Pi OS
You need an up to date copy of [Raspberry Pi OS](https://www.raspberrypi.org/software/) or any other **Linux** distro running on your Rapsberry Pi.

### UI
For the UI we use the [gtk-ui](https://github.com/Jutta-Proto/gtk-ui). Head over there and have a look at the dependencies there.
