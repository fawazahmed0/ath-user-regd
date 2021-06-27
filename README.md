# ath-user-regd

Use DKMS to patch in-tree Atheros wireless driver with OpenWrt `ATH_USR_REGD` for 802.11ac in AP mode

The [OpenWrt](https://openwrt.org/) project provides some patches to the Linux kernel drivers for Atheros wireless chipsets that enable us to broadcast on 5GHz, something that is usually not possible due to regulatory domain limitations that are hard-coded into most desktop and laptop WiFi modules.

DISCLAIMER
---
**I accept no responsibility regarding the legality of using this code. The onus is on YOU to determine on which frequencies and at what power levels you may legally broadcast RF signals in your country or region.**

---

## Installation

First you must download the Linux kernel source and extract it into `./src/linux`. A helper target is available that can do this for you based on the running kernel, or alternatively with the optional argument `KVER`:

```sh
$ make download-src [KVER=5.2]
```
**NOTE** that if specifying `KVER`, it must be specified for *all subsequent commands*. It's also not guaranteed to build if `KVER` is more than one or two minor versions away from the running kernel.

Next, install the DKMS module so that the patched module source gets re-compiled on each kernel update:

```sh
$ sudo make dkms-install
```

To completely remove the patched module from your system and restore the original module:

```sh
sudo make dkms-remove
```

If you are using a rolling release distribution or if you upgrade your major kernel version, you may need to remove and re-install the DKMS script.

Tested and confirmed working on kernels 4.15 and 5.8. Will probably work on anything in between.

Other reference: https://medium.com/@renaudcerrato/how-to-build-your-own-wireless-router-from-scratch-part-3-d54eecce157f
