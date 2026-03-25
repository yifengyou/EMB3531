# rockchip-linux仓库develop-6.6内核

## 基本信息

```shell

root@armbian:~# uname -a
Linux armbian 6.6.89-kdev #1 SMP Wed Mar 25 04:56:28 UTC 2026 aarch64 GNU/Linux
root@armbian:~# 
root@armbian:~# lsusb -t
/:  Bus 001.Port 001: Dev 001, Class=root_hub, Driver=ehci-platform/1p, 480M
/:  Bus 002.Port 001: Dev 001, Class=root_hub, Driver=ehci-platform/1p, 480M
/:  Bus 003.Port 001: Dev 001, Class=root_hub, Driver=xhci-hcd/1p, 480M
/:  Bus 004.Port 001: Dev 001, Class=root_hub, Driver=ohci-platform/1p, 12M
/:  Bus 005.Port 001: Dev 001, Class=root_hub, Driver=ohci-platform/1p, 12M
    |__ Port 001: Dev 002, If 0, Class=Communications, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 1, Class=CDC Data, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 2, Class=Communications, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 3, Class=CDC Data, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 4, Class=Communications, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 5, Class=CDC Data, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 6, Class=Communications, Driver=cdc_acm, 12M
    |__ Port 001: Dev 002, If 7, Class=CDC Data, Driver=cdc_acm, 12M
/:  Bus 006.Port 001: Dev 001, Class=root_hub, Driver=xhci-hcd/1p, 5000M
/:  Bus 007.Port 001: Dev 001, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 008.Port 001: Dev 001, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 5000M
root@armbian:~# 
root@armbian:~# lspci -nn
root@armbian:~# 
root@armbian:~# 


root@armbian:~# inxi -Fxxxz
System:
  Kernel: 6.6.89-kdev arch: aarch64 bits: 64 compiler: gcc v: 11.4.0 clocksource: arch_sys_counter
  Console: pty pts/0 Distro: Armbian 26.02.0-trunk forky
Machine:
  Type: ARM System: Rockchip EMB3531 details: N/A
CPU:
  Info: 6-core model: N/A variant-1: cortex-a72 variant-2: cortex-a53 bits: 64 type: MCP
    smt: <unsupported> arch: ARMv8 rev: 4
  Speed (MHz): avg: 1416 min/max: 408/1416:1800 cores: 1: 1416 2: 1416 3: 1416 4: 1416 5: 1416
    6: 1416 bogomips: N/A
  Features: Use -f option to see features
Graphics:
  Device-1: display-subsystem driver: N/A bus-ID: N/A chip-ID: rockchip:display-subsystem
    class-ID: display-subsystem
  Device-2: rk3399-dw-hdmi driver: dwhdmi_rockchip v: N/A bus-ID: N/A chip-ID: rockchip:ff940000
    class-ID: hdmi
  Device-3: malit860 driver: midgard v: N/A bus-ID: N/A chip-ID: arm:ff9a0000 class-ID: gpu
  Display: unspecified server: N/A driver: N/A tty: 156x35
  API: N/A Message: No API data available in console. Headless machine?
  Info: Tools: No graphics tools found.
Audio:
  Device-1: simple-audio-card driver: asoc_simple_card bus-ID: N/A
    chip-ID: simple-audio-card:es8316-sound class-ID: es8316-sound
  Device-2: rk3399-dw-hdmi driver: dwhdmi_rockchip bus-ID: N/A chip-ID: rockchip:ff940000
    class-ID: hdmi
  Device-3: simple-audio-card driver: N/A bus-ID: N/A chip-ID: simple-audio-card:hdmi-sound
    class-ID: hdmi-sound
  API: ALSA v: k6.6.89-kdev status: kernel-api
Network:
  Device-1: rk3399-gmac driver: rk_gmac_dwmac v: N/A port: N/A bus-ID: N/A
    chip-ID: rockchip:fe300000 class-ID: ethernet
  IF: eth0 state: up speed: 1000 Mbps duplex: full mac: <filter>
Drives:
  Local Storage: total: 14.68 GiB used: 1.93 GiB (13.2%)
  ID-1: /dev/mmcblk0 vendor: Hynix model: HAG4a2 size: 14.68 GiB type: Removable tech: SSD
    serial: <filter> fw-rev: 0x8 scheme: GPT
Partition:
  ID-1: / size: 13.87 GiB used: 1.93 GiB (13.9%) fs: ext4 dev: /dev/mmcblk0p4
  ID-2: /var/log size: 46.8 MiB used: 612 KiB (1.3%) fs: ext4 dev: /dev/zram1
Swap:
  ID-1: swap-1 type: zram size: 949.6 MiB used: 0 KiB (0.0%) priority: 5 dev: /dev/zram0
Sensors:
  System Temperatures: cpu: 36.2 C mobo: N/A
  Fan Speeds (rpm): N/A
Info:
  Memory: total: 2 GiB available: 1.85 GiB used: 175 MiB (9.2%)
  Processes: 140 Power: uptime: 1h 28m states: freeze,mem suspend: deep wakeups: 0 Init: systemd
    v: 259 default: graphical
  Packages: pm: dpkg pkgs: 493 Compilers: gcc: 15.2.0 Shell: Bash v: 5.3.3
    running-in: pty pts/0 (SSH) inxi: 3.3.40

```