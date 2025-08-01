# NVRIMPT

## Description

This guide walks through setting up and provisioning a multi-camera IP surveillance system using Hikvision-compatible cameras, a PoE switch, unmanaged switch, and LTS NVR. By the end of the process, you'll have multiple cameras assigned with static IPs, mapped via spreadsheet, and streaming live to a central NVR. At least I got all the cams talking lol.

---

## Table of Contents

* [Project Setup](#project-setup)
* [Camera and NVR Hardware Overview](#camera-and-nvr-hardware-overview)
* [Steps to Configure Each Camera](#steps-to-configure-each-camera)
* [Spreadsheet IP Mapping](#spreadsheet-ip-mapping)
* [NVR Integration](#nvr-integration)
* [Testing](#testing)
* [Troubleshooting](#troubleshooting)
* [License](#license)

---

## Project Setup

### Requirements

* Hikvision-compatible IP cameras (IPC324ER3-DVPF28, VSIP7442W-28S, CMIP7342W-28M)
* BV 8-Port PoE Switch
* Unmanaged Gigabit Switch
* LTS NVR (e.g. LTN8708-P8)
* SADP Tool installed on a laptop
* Ethernet cables
* Static IP subnet defined (192.168.1.x)
* Google Sheets (for IP mapping)

---

## Camera and NVR Hardware Overview

I worked with a stack of dome cameras labeled CAM-01 through CAM-11, using a BV PoE switch to power and connect them, and an LTS NVR to manage the streams. Here's what the physical setup looked like:

![Workspace Overview](/images/overviewstp.jpg)

![PoE Switch and CAM-10](/images/poeswitch.jpg)

![LTS NVR Unit](/images/recorder.jpg)

---

## Steps to Configure Each Camera

### 1. Connect Camera to PoE Switch

Each camera was plugged into the PoE switch which powered it up and allowed for network communication.

### 2. Discover Camera with SADP Tool

The SADP Tool was launched on my laptop to find all connected cameras. Their default IPs (usually 192.168.1.64) and MAC addresses were recorded.

![Spreadsheet Planning](/images/spreadsheet.jpg)

### 3. Log Into Camera Admin Panel

I accessed the camera UI via browser at its IP address (example: [http://192.168.1.29](http://192.168.1.29)). The login panel provided access to network settings and live view.

![Camera Web UI](/images/adminpanel.jpg)

### 4. Change IP and Subnet

Inside the **Network > Basic Info** section, I:

* Assigned a static IP
* Set subnet mask to 255.255.255.0
* Configured gateway to 192.168.1.1 if needed

Then saved changes and rebooted the camera.

### 5. Confirm Live Feed

Cameras were tested through NVMS7000 and live video was confirmed before moving on to the next device.

---

## Spreadsheet IP Mapping

All planning and documentation were done in a Google Sheet. The sheet helped track:

* Original IPs
* Target static IPs
* Camera model types
* Serial numbers and MACs
* Comments on status (e.g., "GATEWAY REQUIRED")

![IP Planning Sheet](/images/iprange.jpg)

---

## NVR Integration

### 1. Connect NVR to Unmanaged Switch

The LTS NVR was connected to the unmanaged switch to receive streams from all IP cameras via the PoE uplink.

### 2. Access Camera Config on NVR

Through the NVR interface:

* Navigated to **Camera > Add Camera**
* Added each camera's static IP manually
* Used ONVIF protocol for compatibility
* Assigned each camera to an appropriate channel

![Initial Camera Discovery on NVR](/images/initialnvr.jpg)

### 3. Finalize Settings

I verified frame rates, adjusted recording schedules, and ensured storage detection was successful. Each stream was confirmed via HDMI monitor.

---

## Testing

All camera feeds were tested across three systems:

* **Browser UI**: Confirmed admin access, motion detection, and live view
* **NVMS7000**: Used for layout view and playback verification
* **LTS NVR**: Confirmed centralized control, playback, and export features

![Project Desk & Live Testing](/images/setupstation.jpg)

---

## Troubleshooting

### Issue 1: SADP doesn't detect camera

* **Fix**: Restart PoE switch, or directly connect the camera to the laptop NIC.

### Issue 2: IP conflict with reused defaults

* **Fix**: Reference spreadsheet; reset camera using SADP or physical button.

### Issue 3: NVR says "Offline"

* **Fix**: Confirm camera’s IP, gateway, and port (should be 8000). Also re-check ONVIF password.

### Issue 4: Camera inaccessible via browser

* **Fix**: Clear browser cache, verify subnet alignment, use IP scanner if unsure.

---

## License

This documentation is open-source and intended for lab, educational, and professional use. Feel free to replicate or fork. Just don’t forget to label your cables.
