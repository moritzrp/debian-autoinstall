# Debian Autoinstall

Resources for creating a custom Debian image which applies a preseed config.

## Useful Documentation

- [Automating the installation using preseeding](https://www.debian.org/releases/stable/riscv64/apb.en.html)
- [Contents of the preconfiguration file](https://www.debian.org/releases/stable/amd64/apbs04.en.html)
- [Using the Debian Installer](https://www.debian.org/releases/stable/amd64/ch06.en.html)

## Steps

1. Run `preseed-initrds` to create new initrds
2. Build new custom image

```bash
xorriso \
  -indev debian-13.2.0-amd64-netinst.iso \
  -outdev debian-13.2.0-preseed.iso \
  -boot_image any replay \
  -map out/install.amd/initrd.gz /install.amd/initrd.gz \
  -map out/install.amd/gtk/initrd.gz /install.amd/gtk/initrd.gz \
  -map isolinux/adtxt.cfg /isolinux/adtxt.cfg \
  -map isolinux/spkgtk.cfg /isolinux/spkgtk.cfg \
  -map isolinux/menu.cfg /isolinux/menu.cfg
```

## What it does

- Creates new `initrd.gz` with `preseed.cfg` file added
- Updates the BIOS menus to start the auto installation after 5 seconds delay

## TODOs

- Creating custom `initrd.gz` is probably not necessary.
  Instead, add `preseed.cfg` to ISO and update menu to start referencing the file from CD
