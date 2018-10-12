# Ultimate Raspberry Pi 3 Entertainment System

## What the purpose of this?

I spend a lot of time looking for projects to archive the goal of having a Raspberry on my TV room to play games and do some other stuff like blocking ads...

## After the steps, what I get?

- AdBlocker for your home Network(using Pi Hole)
- Monitoring Dashbord for Raspberry CPU, Memory...
- Game streaming using Nvidia Stream technology (Moonlight Embedded Project)

## Pre-requisites

1. Access through SSH to your Raspberry
2. A gamer desktop to proccess your games
3. Configure your game's shortcuts on PC to be open inside Steam
4. Bluetooth gamepads (I'm using Xbox One S controllers)

## What I need to do?

This guide is separated in 4 steps:

1. Configure Pi Hole
2. Configure the dashbaord to check raspberry resources (CPU, Mem...)
3a. Configure xPadNeo to use Xbox One S controllers
3b. Configure Moonlight Embedded to play games from your Desktop

## 1. Configure Pi hole ([link to project](https://pi-hole.net/))

This is the most straight foward of all.
You just need to run `curl -sSL https://install.pi-hole.net | bash` and follow the steps provided on the wizard

## 2. Configuring the dashboard for Raspberry

This process is easy to follow too, just paste and copy the following commands:

Install `dirmngr` package

```
$ sudo apt-get install dirmngr
```

Configure the public keys for the repository

```
$ sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 2C0D3C0F
$ sudo wget http://goo.gl/vewCLL -O /etc/apt/sources.list.d/rpimonitor.list
```

Update packages and install from repository

```
$ sudo apt-get update
$ sudo apt-get install rpimonitor
```

(Optional) If you want to show deprecated packages installed on your Raspberry, use this command

```
$ sudo /etc/init.d/rpimonitor update
```

Done, you can access the dashboard from this address:

```
http://[raspberry_ip]:8888
```

## 3a. Configure xPadNeo to use Xbox One S Controllers  ([link to project](https://github.com/atar-axis/xpadneo))

The first step is to configure your raspberry with the last updates for `dkms` and `kernel-headers`

```
$ sudo apt-get install dkms raspberrypi-kernel-headers
```

Then, after this, you can clone the project and install

```
$ git clone https://github.com/atar-axis/xpadneo.git && cd xpadneo && ./install.sh
```

Just to be sure everything will be loaded fine, restart your raspberry

```
$ sudo reboot
```

Then you must pair the xbox controller (bluetooth version) with your raspberry

```
$ sudo bluetoothctl

[bluetooth]# scan on
[bluetooth]# pair <CONTROLLER_MAC>
[bluetooth]# trust <CONTROLLER_MAC>
[bluetooth]# connect <CONTROLLER_MAC>
```
## 3b. Configure Moonlight Embedded project

First you need to add package's to repositories list

```
$ sudo nano /etc/apt/sources.list
```

Copy and paste this line (if you're using raspbian strech)

``` 
deb http://archive.itimmer.nl/raspbian/moonlight stretch main
```

Then, install the GPG key
```
$ wget http://archive.itimmer.nl/itimmer.gpg && sudo apt-key add itimmer.gpg
```

Update packages and finally install moonlight-stream

```
$ sudo apt-get update && sudo apt-get install moonlight-embedded
```

Pair your moonlight client with your Nvidia GPU using (the 4 number code will be inserted on your streaming machine)

```
$ moonlight pair
```

I found that the best configuration for my raspberry is the following, but you can play with numbers too.
All the info is on ([this link](https://github.com/irtimmer/moonlight-embedded/wiki/Usage))
```
$ moonlight stream -1080 -fps 60 -bitrate 7500 -nosops
```
