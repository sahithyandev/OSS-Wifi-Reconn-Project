# CS3460 — Operating Systems Security: WiFi Reconnaissance Project

**Student:** Sahithyan K. (230557T)  
**Topic:** Conducting Wi-Fi Reconnaissance Using the Aircrack-ng Suite

## Overview

This project demonstrates passive and active Wi-Fi reconnaissance techniques using the Aircrack-ng toolchain. The work was performed on a friend's Ubuntu laptop (the MacBook's built-in adapter doesn't support monitor mode or packet injection).

The reconnaissance covered: SSID/BSSID enumeration, channel and encryption profiling, signal strength mapping, connected client discovery, packet capture on a targeted AP, and WPA/WPA2 handshake capture via deauthentication.

## Setup

The project ran on **Ubuntu** with the following prerequisites:

```sh
sudo apt install aircrack-ng   # install the suite
iwconfig                       # verify wireless interface (wlp2s0)
sudo airmon-ng check kill      # kill interfering processes (wpa_supplicant, avahi-daemon)
sudo airmon-ng start wlp2s0    # enable monitor mode → interface becomes wlp2s0mon
```

## Workflow

| Step | Command | Output |
|------|---------|--------|
| Scan all APs | `sudo airodump-ng wlp2s0mon` | SSIDs, BSSIDs, channels, encryption |
| Target an AP | `sudo airodump-ng -c <ch> --bssid <mac> -w capture wlp2s0mon` | `captures/capture-01.*` |
| Deauth clients | `sudo aireplay-ng -0 5 -a <bssid> wlp2s0mon` | forces WPA handshake re-exchange |

Six scan sessions were collected under `scans/` and one packet capture under `captures/`.

## File Structure

```
project/
├── README.md
├── justfile                    # build commands (tectonic for LaTeX)
│
├── report.tex                  # LaTeX source
├── report.pdf                  # compiled report
│
├── logs/                       # terminal session transcripts
│   ├── oss-wifi-reconn.txt     # session 1 — initial recon setup
│   ├── oss-reconn-2.txt        # session 2
│   └── oss-reconn-3.txt        # session 3
│
├── captures/                   # raw wireless capture data
│   ├── capture-01.cap          # packet capture (Wireshark/tcpdump format)
│   ├── capture-01.csv          # airodump-ng CSV output
│   ├── capture-01.log.csv      # airodump-ng log CSV
│   ├── capture-01.kismet.csv   # Kismet CSV export
│   └── capture-01.kismet.netxml# Kismet network XML
│
├── scans/                      # airodump-ng scan results (6 sessions)
│   ├── wifi_recon-01.csv … wifi_recon-06.csv
│   └── wifi_recon-01.kismet.csv … wifi_recon-06.kismet.csv
│
└── screenshots/                # supporting screenshots (Kismet UI, terminal)
```

## Build

```sh
just build   # compiles report.tex → report.pdf using tectonic
just clean   # removes report.pdf
```

## Tools Used

- **airmon-ng** — enable/disable monitor mode on the wireless adapter
- **airodump-ng** — passive AP/client scanning and packet capture
- **aireplay-ng** — deauthentication attacks (forces WPA handshake capture)
- **Kismet** — passive WiFi scanning (supplementary)
- **Wireshark / tcpdump** — offline packet analysis (`.cap` files)
- **Tectonic** — LaTeX compiler for the report
