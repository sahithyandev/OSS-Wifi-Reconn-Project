# CS3460 — Operating Systems Security: WiFi Reconnaissance Project

## File Structure

```
project/
├── README.md                   # This file
├── justfile                    # Build commands (tectonic for LaTeX)
│
├── report.tex                  # LaTeX source for the project report
├── report.pdf                  # Compiled report
│
├── logs/                       # Terminal session transcripts
│   ├── oss-wifi-reconn.txt     # Session 1 — initial recon setup
│   ├── oss-reconn-2.txt        # Session 2
│   └── oss-reconn-3.txt        # Session 3
│
├── captures/                   # Raw wireless capture data
│   ├── capture-01.cap          # Packet capture (Wireshark/tcpdump format)
│   ├── capture-01.csv          # Airodump-ng CSV output
│   ├── capture-01.log.csv      # Airodump-ng log CSV
│   ├── capture-01.kismet.csv   # Kismet CSV export
│   └── capture-01.kismet.netxml# Kismet network XML
│
├── scans/                      # Kismet WiFi scan results (per session)
│   ├── wifi_recon-01.csv
│   ├── wifi_recon-01.kismet.csv
│   ├── wifi_recon-02.csv
│   ├── wifi_recon-02.kismet.csv
│   ├── wifi_recon-03.csv
│   ├── wifi_recon-03.kismet.csv
│   ├── wifi_recon-04.csv
│   ├── wifi_recon-04.kismet.csv
│   ├── wifi_recon-05.csv
│   ├── wifi_recon-05.kismet.csv
│   ├── wifi_recon-06.csv
│   └── wifi_recon-06.kismet.csv
│
└── screenshots/                # Supporting screenshots
    ├── Screenshot from 2026-05-16 12-25-57.png
    ├── Screenshot from 2026-05-16 12-26-13.png
    ├── Screenshot from 2026-05-16 12-45-40.png
    └── Screenshot from 2026-05-16 13-17-02.png
```

## Build

```sh
just build   # compiles report.tex → report.pdf using tectonic
```

## Tools Used

- **airmon-ng / airodump-ng** — monitor mode and packet capture
- **Kismet** — passive WiFi scanning
- **Wireshark / tcpdump** — packet analysis (`.cap` files)
- **Tectonic** — LaTeX compiler for the report
