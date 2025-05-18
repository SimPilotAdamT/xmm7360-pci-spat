⚠️ _*In heavy development. Basic support provided. May not work, may crash your computer, may singe your jaffles.*_ ⚠️

# Getting started

## What

Driver for Fibocom L850-GL / Intel XMM7360 (PCI ID 8086:7360).

Please see [DEVICES.md](DEVICES.md) a list of devices this has been tested on.

This specific fork fixes issues with building the package as the AUR packages work at the moment. I will be archiving this repo once integration with ModemManager has been implemented. This is being tracked in [#255](https://github.com/xmm7360/xmm7360-pci/issues/225). The pending implementation in ModemManager is the reason why I haven't created a pull request to commit my changes upstream.

## How

Please see [INSTALLING.md](INSTALLING.md) for details on how to setup this driver on your system.

## Status

This release supports native IP.

To test:

- `sudo pip install --user pyroute2 ConfigArgParse`
- `make && make load`
- If your sim has pin enabled, run `echo "AT+CPIN=\"0000\"" | sudo tee -a /dev/ttyXMM1`. Replace `0000` with your pin code.
- `sudo python3 rpc/open_xdatachannel.py --apn your.apn.here` (or you can create the xmm7360.ini from the sample and edit the apn)
- pray (if applicable)

> If your sim has pin enabled, run `echo "AT+CPIN=\"0000\"" | sudo tee -a /dev/ttyXMM1`. Replace `0000` with your pin code.

You should receive a `wwan0` interface, with an IP, and a default route.

## Next

Involvement from someone involved in modem control projects like ModemManager
would be welcome to shape the kernel interfaces so it's not too horrible to
bring up.

Power management support is absent. The modem, as configured, turns off during
suspend, and needs to be reconfigured on resume.
