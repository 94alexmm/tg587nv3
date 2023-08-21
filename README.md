# Technicolor TG587N v3 (Telstra Bigpond router)
Modifying and gaining root access on the Thomson/Technicolor TG587Nv3.

The router uses a modified version of OpenWRT

| Method | Works | Notes |
|--|--|--|
|AutoFlashGUI | **Not working** |  Tested with a password set and it authenticates but has no effect after restart.|
TchExploit | **Working** | Follow steps as outlined. https://github.com/BoLaMN/tch-exploit Note you need to use 10.0.0.138:22 when opening SSH connection after exploit not 192.* as stated |

## Specs

Broadcom BMIPS4350 V7.0

<img width="392" alt="image" src="https://github.com/94alexmm/tg587nv3/assets/15701642/55b850f9-6f76-4d76-b53e-da8be4da2fbc">

## Opening an SSH session
Once modified using TchExploit you must use an override flag as the router does not support any secure key exchanges.

```
 ssh -o KexAlgorithms=diffie-hellman-group1-sha1 root@10.0.0.138
```

![image](https://github.com/94alexmm/tg587nv3/assets/15701642/29c1156d-2de1-4996-8d3a-72528b53bc53)

## Installing new packages
Open the opkg config
```
vi /etc/opkg.conf
```

Replace repo URL with non technicolor URL
```
https://archive.openwrt.org/attitude_adjustment/12.09/brcm63xx/generic/packages
```
Save

Run 
```
opkg update
```

Add the following lines (Need to change architecture src = https://alastair.d-silva.org/technicolor-tg789vac-v2-root-access)
```
arch all 1
arch noarch 1
arch brcm63xx 3
arch brcm63xx-tch 10
```
