# Initial deployment

Initial flashing of Dasharo firmware can be done from Linux using flashrom with
the internal programmer. This document describes the process of building,
installing and running flashrom on Ubuntu 22.04.

## Deploy using Dasharo Tools Suite

For simplicity we recommend using
[Dasharo Tools Suite](../../../common-coreboot-docs/dasharo_tools_suite) to
omit all compilation steps and deploy the Dasharo firmware seamlessly.
Be sure to disable the BIOS lock in the AMI firmware setup utility:

1. Go to `Chipset` tab
2. Enter `PCH IO Configuration`
3. Disable `BIOS Lock`.
4. Save changes and reset.

Now you are ready to use Dasharo Tools Suite (DTS):

1. Boot Dasharo Tools Suite.
2. Perform Dasharo installation.

## Build flashrom

Currently, the latest flashrom release lacks support for Comet Lake U internal
flashing. Because of this, we need to build flashrom from source.

Install build dependencies:

```bash
apt install git build-essential debhelper pkg-config libpci-dev libusb-1.0-0-dev libftdi1-dev meson
```

Obtain source code:

```bash
git clone https://github.com/Dasharo/flashrom -b dasharo-release
cd flashrom
```

Build flashrom:

```bash
sudo make install
```

## Reading flash contents

Always prepare a backup of the current firmware image. To read from the flash
and save them to a file (`backup.rom`), execute the following command:

```bash
flashrom -p internal -r dump.rom
```

Keep the backup for later recovery if needed.

## Flashing Dasharo

To flash Dasharo on the platform, execute the following command - replace
`[path]` with the path to the Dasharo image you want to flash, e.g.
`protectli_vault_ehl_v1.0.0.rom`.

If stock firmware is currently installed:

```bash
flashrom -p internal -w [path] --ifd -i bios
```

If Dasharo is currently installed, only the `RW_SECTION_A` partition of the
flash needs to be updated. Flash it using the following command:

```bash
flashrom -p internal -w protectli_vault_ehl_v1.x.y.rom --fmap -i RW_SECTION_A
```

This command also preserves Dasharo UEFI settings and the boot order.
