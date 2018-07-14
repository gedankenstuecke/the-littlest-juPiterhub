# How to set-up the Raspberry Pi Zero W with Raspian Stretch
First steps: [Download a Raspian image](https://www.raspberrypi.org/downloads/raspbian/) and flash it onto a SD card [using Etcher or whatever](https://etcher.io/) other tool you prefer.

## Autoconnect to WiFi & Enable SSH
(based on [this useful article](https://core-electronics.com.au/tutorials/raspberry-pi-zerow-headless-wifi-setup.html)).

- mount your flashed SD card on your regular computer, will show up as `boot`
- in the root folder of the SD card create a file called `wpa_supplicant.conf`

Enter the following in the file, and adjust `ssid` and `psk` with your Wifi's name & passphrase:

```
country=us
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 scan_ssid=1
 ssid="MyNetworkSSID"
 psk="Pa55w0rd1234"
}
```

To also enable `ssh` access to the machine create an empty file called `ssh` in the root folder of the SD card.

## Boot the Pi & connect
Now you can slide your SD card into the Pi and power it up. Once it's booted you can SSH into it by using

```
ssh pi@raspberrypi.local
```

The standard password is `raspberry`. Once you're connected you should run

```
sudo raspi-config
```

and change things like the `hostname`, `password` etc. Also make sure that you permanently enable the `ssh` access here!

## Installing Conda
Continuum doesn't provide versions for *ARM* chips, but luckily there's [berryconda](https://github.com/jjhelmus/berryconda), which has versions for ARM6 & ARM7. Download whichever version you need to your Pi and run it.

```
wget https://github.com/jjhelmus/berryconda/releases/download/v2.0.0/Berryconda3-2.0.0-Linux-armv6l.sh
bash Berryconda3-2.0.0-Linux-armv6l.sh
```

You're all good for installing conda/python packages now. 🎉
