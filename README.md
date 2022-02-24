# Hardened Dafang Hacks Custom Firmware | RTSP server

The goal of this repository is to create a hardened, stable, and performant fork of [dafang-hacks](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks.git) with plain-old RTSP server on a minimal stripped-down linux runtime environment. External internet-based network services (ex. Telegram, MQTT, HomeKit, etc) have been stripped out.

As the devices may execute unaudited binary blobs, place them in a closed-circuit offline loop (CCTV) with a locally provisioned RTSP gateway and Time Server.

Refer to section on [Security](Security).

## Device Support

Firmware has been tested stable on the following devices if using releases based on `master` branch.

Name | Picture
--- | ---
Wyzecam V2 | ![XiaoFang](/xiaofang.png)

Refer to [device support](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks) for the full list. Note forked firmware may brick your device and you assume all responsibility for usage.

### WARNING: Do not install the latest Firmware on your Device. It will prevent installing custom firmware.

See upstream [issue #669](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/issues/669).

### Flashing Firmware

1. Before you try to install it, please read the [FAQ](/hacks/faq.md)
2. After that, continue to the [Installation](/hacks/install_cfw.md)

Technical docs on cfw flashing process can be found [here](/hacks/technical.md)

--- 

## Capturing Feed

Using any open source RTSP server, point the capture url to `rtsp://<IP_ADDRESS>:8554/unicast`, where the `<IP_ADDRESS>` is either `DHCP_LEASE_IP` or `HOSTAPD_DHCP_SERVER_IP = 10.0.0.1`.

### Supported Integrations

Locally running services on the same network can access camera feed/controls.

* [Custom Scripts](/integration/custom/motiondetection.md)
* [Zoneminder](/integration/zoneminder/zoneminder.md)

---

## Security

Hardening entails both auditing the original source (work in progress) for potential vulnerabilities and minimizing the attack surface.

### Functionality Removed

Complete list of internet-based services including those defined as [malware](https://gnu.org/malware) removed:

* Outbound/Matrix
* Outbound/Telegram
* Integration/HomeAutomation
* Integration/Homekit
* Integration/Openhab
* Service/AutoUpdate
* Service/MQTT
* Service/Telnet
* Service/Mail
* Service/hostapd

### RFC: Planned Removal

To further harden, the webserver should be optional. In place, SSH server can be bound to auto-start for modifying configuration remotely.

LetsEncrypt pre-generated certificate.

### RFC: Pending Audit

* [C libs - /firmware_mod/lib/.so](/firmware_mod/lib/)
* [bin - /firmware_mod/bin/](/firmware_mod/bin/)
* [driver bins - /firmware_mod/driver_t20l](/firmware_mod/driver_t20l/)
* [minified hls js bundle - /firmware_mod/hls/](/firmware_mod/hls/)
* [js bundles - /firmware_mod/www/lib](/firmware_mod/www/lib)

**Libaries**

Sources include static [libaries](/firmware_mod/www/lib) with `sha256sum` hashes to verify originals against publically available compiled releases.

**Binary Blobs**

Based on licensing issues (described below), "binary blobs" for bootloader and original firmware have been stripped out. Sources can be obtained from upstream repo [Xiaomi-Dafang-Hacks](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/) and verified against `sha256sum` `sha3sum`.

----

## Contributing

Issues and pull-requests are welcome. Please report the usage of insecure linked libraries or configs. 

----

## LICENSE

Fork is licensed as "for the work that has happened inside this repo, you can assume a very free license" [source](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/issues/1379) and "any contribution to the development is highly welcome" [readme](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/).

The upstream license of certain components remain unclear, see the following issues:

* [Issue #974 - Please add MIT license](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/issues/974)
* [Issue #1379 - license of this project](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/issues/1379)
* [Issue #1763 - License?](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/issues/1763)

View `git commit` history tree to determine what constitutes under appropriate license.
