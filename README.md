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
In the [3D-printer](3D-printer/README.md) directory you can find more information about how to print a case for the Raspberry Pi, its display and attache it to the coffee maker.

## Software
In this section we have a look at the software required for this.

### Raspberry Pi OS
You need an up to date copy of [Raspberry Pi OS](https://www.raspberrypi.org/software/) or any other **Linux** distro running on your Rapsberry Pi.

### UI
For the UI we use the [gtk-ui](https://github.com/Jutta-Proto/gtk-ui). Head over there and have a look at the dependencies there.

### Installing
Here we have a look at what needs to be done when setting up a up to date copy of [Raspberry Pi OS](https://www.raspberrypi.org/software/) to work with this project.

#### Installing Clang
**⚠This is not requied any more for recent releases of Raspberry Pi OS.⚠**

Since the out of the box available C++ compilers for the Raspberry Pi a bit to old and therefore unable to compile C++20 code, we are installing our own, up to date compiler. We decided to use [Clang](https://clang.llvm.org/) instead of [gcc](https://gcc.gnu.org/), since it's easier to set up on a Raspberry Pi. 
```bash
sudo apt remove -y gcc clang # Remove all old compilers
wget https://github.com/llvm/llvm-project/releases/download/llvmorg-12.0.0/clang+llvm-12.0.0-armv7a-linux-gnueabihf.tar.xz
tar -xvf clang+llvm-12.0.0-armv7a-linux-gnueabihf.tar.xz
rm clang+llvm-12.0.0-armv7a-linux-gnueabihf.tar.xz
mv clang+llvm-12.0.0-armv7a-linux-gnueabihf clang_12.0.0
sudo mv clang_12.0.0 /usr/local
echo 'export PATH=/usr/local/clang_12.0.0/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/clang_12.0.0/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
. ~/.bashrc
```

Once the installation was successful, you can test it with:
```bash
clang++ --version
```

#### Enabling UART
To the enable UART (serial communication) on the Raspberry Pi, perform the following steps:
* `sudo raspi-config`
* Select `Interface Options`
* Select `Serial Port`
* Select `No` to prevent the Pi from using the serial port for the login shell.
* Select `Yes` to enable the serial port hardware.
* Select `OK`
* Select `Finish`
* Select `No` in case it asks you if you want to reboot now.

Now we add our self to the `dialout` group, so we do not need sudo to access the serial port.
```bash
sudo usermod -a -G dialout pi
```
And finally reboot.
```bash
sudo reboot -h now
```

### Other Requirements
There are a few shared requirements needed by all projects.
```bash
sudo apt install -y git cmake make ninja-build python3 python3-pip
pip3 install --user conan==1.59.0 # conan 2.x.x is not supported right now
```

## Connecting a Coffee Maker
The following image shows how to connect the Raspberry Pi with an JURA E6 coffee maker.
![Pinout_Raspberry_Pi](https://user-images.githubusercontent.com/11741404/120469237-631e9900-c3a2-11eb-9f2e-731905ed8138.png)
Since the Raspberry Pi can only handle 3.3V UART signals, we need a "Logic Level Shifter" in between the coffee maker and the Raspberry Pi.
