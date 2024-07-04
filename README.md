- ### Install OpenWrt

1. For the `Rockchip` platform, please refer to the [Chapter 8](https://github.com/ophub/amlogic-s9xxx-armbian/blob/main/documents/README.md#8-installing-armbian-to-emmc) of the instruction manual, the installation method is the same as that of Armbian.

2. For the `Amlogic` and `Allwinner` platforms, use tools like [Rufus](https://rufus.ie/) or [balenaEtcher](https://www.balena.io/etcher/) to write the firmware to USB, then insert the USB with the written firmware into the box. Browser access to OpenWrt's IP (e.g. 192.168.1.1) → `Log in to OpenWrt with the default account` → `System Menu` → `Amlogic Treasure Box` → `Install OpenWrt`, select your box from the dropdown list of supported devices, click `Install OpenWrt` button to install.

- ### Update OpenWrt system or kernel

Browser access to OpenWrt's IP (e.g. 192.168.1.1) → `Log in to OpenWrt with your account` → `System Menu` → `Amlogic Treasure Box` → `Manually Upload Update / Online Download Update`

If you select `Manually Upload Update` [OpenWrt Firmware](https://github.com/ophub/amlogic-s9xxx-openwrt/releases), you can upload the compressed package of the compiled OpenWrt firmware, such as openwrt_xxx_k5.15.50.img.gz (recommended to upload the compressed package, the system will automatically decompress. If you upload the decompressed xxx.img format file, it may fail due to the large file size). After the upload is complete, the interface will display the operation button of `Update Firmware`, click to update.

If you select `Manually Upload Update` [OpenWrt Kernel](https://github.com/ophub/kernel/releases/tag/kernel_stable), you can upload the three kernel files: `boot-xxx.tar.gz`, `dtb-xxx.tar.gz`, `modules-xxx.tar.gz` (other kernel files are not needed, if uploaded simultaneously, it does not affect the update, the system can accurately identify the needed kernel files). After the upload is complete, the interface will display the operation button of `Update Kernel`, click to update. When a kernel update failure causes the system to be unbootable, you can use the `openwrt-kernel -s` command for kernel recovery. For the method, see [Kernel Recovery](documents/README.md#9-update-openwrt-system-or-kernel).

If you select `Online Download Update` for OpenWrt firmware or kernel, it will be downloaded according to the `firmware download address` and `kernel download address` in the `Plugin Settings`. You can customize the download source. For specific operation methods, please refer to the compilation and usage instructions of [luci-app-amlogic](https://github.com/ophub/luci-app-amlogic).

- ### Create swap for OpenWrt

If you feel that the current box's memory is not enough when using memory-intensive applications like `docker`, you can create a `swap` virtual memory partition, and use a certain capacity of the `/mnt/*4` disk space as memory. The unit of the input parameter in the command below is `GB`, the default is `1`.

Browser access to OpenWrt's IP (e.g. 192.168.1.1) → `Log in to OpenWrt with the default account` → `System Menu` → `TTYD Terminal` → enter the command

```yaml
openwrt-swap 1
```

- ### Backup/Restore Original EMMC System

Supports backing up/restoring the `EMMC` partition of the box in `TF/SD/USB`. We recommend that you backup the Android TV system that comes with the box before installing the OpenWrt system in a brand-new box for future use in restoring the TV system, etc.

Please boot OpenWrt system from `TF/SD/USB`, from the browser, Browser access to OpenWrt's IP (e.g. 192.168.1.1) → `Log in to OpenWrt with the default account` → `System Menu` → `TTYD Terminal` → enter the command

```yaml
openwrt-ddbr
```

Follow the prompts to enter `b` to backup the system, or enter `r` to restore the system.

> [!IMPORTANT]
> In addition, the Android system can also be flashed into eMMC using the method of flashing via a cable. The download image of the Android system can be found in [Tools](https://github.com/ophub/kernel/releases/tag/tools).

- ### Control LED Display

Browser access to OpenWrt's IP (e.g. 192.168.1.1) → `Log in to OpenWrt with the default account` → `System Menu` → `TTYD Terminal` → enter the command

```yaml
openwrt-openvfd
```

Refer to [LED Screen Display Control Description](https://github.com/ophub/amlogic-s9xxx-armbian/blob/main/documents/led_screen_display_control.md) for debugging.

## Default Information for OpenWrt Firmware

| Name | Value |
| ---- | ---- |
| Default IP | 192.168.1.1 |
| Default Account | root |
| Default Password | password |
| Default WIFI Name | OpenWrt |
| Default WIFI Password | None |

## Compile the Kernel

For instructions on how to compile the kernel, see [compile-kernel](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/compile-kernel).

```yaml
- name: Compile the kernel
  uses: ophub/amlogic-s9xxx-armbian@main
  with:
    build_target: kernel
    kernel_version: 6.1.y_5.15.y
    kernel_auto: true
    kernel_sign: -yourname
```


## Links

- [unifreq](https://github.com/unifreq/openwrt_packit)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf](https://github.com/coolsnowwolf/lede)
- [immortalwrt](https://github.com/immortalwrt/immortalwrt)

## License

The amlogic-s9xxx-openwrt © OPHUB is licensed under [GPL-2.0](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/LICENSE)

