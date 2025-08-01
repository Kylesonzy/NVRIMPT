# NVRIMPT

A network video recorder (NVR) and IP camera provisioning project using PoE switches, LTS NVR systems, Hikvision-compatible cameras, and structured IP planning. This setup was deployed for testing and documenting multi-camera infrastructure across isolated VLANs and subnets.

---

## 📦 How It's Built

**Technologies Used:**

- BV 8-Port PoE Switch
- Unmanaged Gigabit Network Switch
- Hikvision IP Cameras (IPC324ER3-DV, CMIP7342W, VSIP7442W)
- LTS Network Video Recorder (NVR)
- NVMS7000 Surveillance Software
- SADP Tool (for IP discovery and provisioning)
- Spreadsheet IP Planning (Google Sheets)
- VLAN Segmentation
- Static IP Assignment

This project documents the full process of provisioning and integrating over 10 IP cameras with an LTS NVR in a lab environment. It includes structured naming conventions, IP schema documentation, and tools used for monitoring and managing the networked surveillance system.

---

## ⚙️ Key Steps

- Unboxed and labeled Hikvision-compatible dome cameras for physical and logical organization.
- Connected cameras to a BV PoE switch and routed uplink to an unmanaged switch for main network access.
- Used **SADP Tool** to identify default IPs and changed each camera's address to static IPs based on a planning spreadsheet.
- Accessed individual camera admin panels (e.g., `192.168.1.29`) to verify model, firmware, and configure network settings.
- Maintained a detailed spreadsheet for mapping camera names, IPs, MACs, serials, and port assignments.
- Verified camera connectivity and video stream ingestion using **NVMS7000** software.
- Registered and configured the **LTS NVR**, ensuring cameras were recording properly with time sync and stream settings applied.
- Segmented camera groups via VLANs for network traffic isolation, improving manageability and security posture.

---

## 🧠 IP Management Strategy

Each camera was provisioned with a unique static IP based on logical zone labeling (e.g., CAM-01 through CAM-11). IP ranges were maintained in a centralized Google Sheet which tracked:

| Camera | Model              | Static IP     | MAC Address       | Serial Number        |
|--------|--------------------|---------------|--------------------|----------------------|
| CAM-01 | CMIP7342W-28M      | 192.168.1.21  | 14:2F:FD:xx:xx:xx  | CMIP7342W-28Mxxxxx   |
| CAM-05 | IPC324ER3-DVPF28   | 192.168.1.25  | 48:EA:63:xx:xx:xx  | IPC324ER3xxxxx       |
| CAM-10 | IPC324ER3-DVPF28   | 192.168.1.30  | 48:EA:63:xx:xx:xx  | IPC324ER3xxxxx       |

This spreadsheet also included annotations for:

- Devices that required gateway or subnet mask corrections
- Cameras on temporary IPs that needed remapping
- VLAN mapping per department or physical zone
- Notes on firmware versions and ONVIF protocol compatibility

---

## 🛠️ Tools Used

- **SADP Tool** – Hikvision’s IP scanner and provisioning utility.
- **NVMS7000** – Monitoring software used to test, visualize, and manage the video feeds.
- **Browser Admin Panels** – For accessing each camera's configuration (192.168.1.x).
- **Google Sheets** – Maintained structured IP/MAC/serial map and configuration tracking.
- **BV PoE Switch** – Delivered power and data to each IP camera through a single line.
- **Unmanaged Gigabit Switch** – Served as the core network backbone for inter-device routing.
- **LTS NVR** – The core recording device receiving, storing, and managing all camera feeds.

---

## 📈 Lessons Learned

- **Proper Planning Prevents Problems** – With over a dozen nearly identical cameras, spreadsheet-based planning saved hours of troubleshooting.
- **PoE Convenience** – Reduced clutter and improved organization by eliminating separate power supplies.
- **IP Conflicts Are Common** – Some default cameras boot with the same IP (192.168.1.64) causing overlap; early remapping is critical.
- **Hardware Behavior Varies** – Certain models needed factory reset or firmware reflash due to boot/response issues.

---

## 🙏 Acknowledgements

Thanks to the Hikvision and LTS development teams for hardware support. Special thanks to the open-source SADP and NVMS7000 developers for tools that made multi-camera provisioning feasible. Also, appreciation to the deployment team for assisting with hardware unboxing, wiring, and real-time NVR testing during configuration.

---

