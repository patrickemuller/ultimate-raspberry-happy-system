# Ultimate Raspberry Pi 3 Entertainment System

## What is this?

This is a guide on how to configure your Raspberry Pi 3 as AdBlocker, NAS server, miniDLNA media server AND Game Station using Nvidia Stream Protocol (only for Nvidia GPUs, sorry...)

## After the steps, what I get?

- AdBlocker (using Pi Hole)
- NAS server using Raspberry
- DLNA server to watch movies or show stuff on SmartTVs
- Game console using your desktop Powerhorse (aka your Nvidia GPU)

## What I need to do?

This guide is separated in 4 steps:
- 1. Configure Pi Hole
- 2a. Configure NAS server
- 2b. Configure DLNA server (to watch downloaded movies)
- 3. Configure Moonlight Embedded to play games from your Desktop

The only Dependencies here is steps 2 and 3, because to have a DLNA server you need to configure the NAS server first.

## 1. Configure Pi hole ([link to project](https://pi-hole.net/))

This is the most straight foward of all.
You just need to run `curl -sSL https://install.pi-hole.net | bash` and follow the steps provided on the wizard

## 2a. Configure NAS Server

WIP

## 2b. Configure miniDLNA

- `sudo apt-get install minidlna`
Now you need to connect the USB driver you gonna use as storage (probably will be the largest one)
- `sudo fdisk -l`

## 4. WIP
