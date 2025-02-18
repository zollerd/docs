# Building manual

## Intro

This document describes the procedure for compiling coreboot for Protectli
VP4630, VP4650 and VP4670.

## Requirements

- Docker
    + follow [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
    + follow [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/)
- Git

## Build Dasharo BIOS firmware

> This build procedure produces full firmware binary including blobs such as
> FSP, and ME. Currently, access to them is restricted to the OEM (Protectli) via
> a private repository.

Since version v1.0.18 VP4630 and VP4650 use different configuration file than
VP4670. Versions v1.0.17 and older do not support VP4650 and VP4670 at all.

1. Clone the coreboot repository:

    ```bash
    git clone https://github.com/Dasharo/coreboot
    ```

1. Checkout the desired version, e.g. `v1.0.19`:

    ```bash
    cd coreboot
    git checkout protectli_vault_cml_v1.0.19
    ```

1. Checkout submodules:

    ```bash
    git submodule update --init --checkout
    ```

1. Obtain the Protectli blobs package:

    > Replace `<PROTECTLI_BLOBS_REPO>` with a a proper path to the repository
    > in a form of: `git@repo-path.git`. You should checkout to the same tag as
    > in case aof the coreboot repository.

    ```bash
    cd 3rdparty/blobs/mainboard/
    git init
    git remote add origin <PROTECTLI_BLOBS_REPO>
    git fetch origin && git checkout protectli_vault_cml_v1.0.19
    cd -
    ```

1. Build the firmware v1.0.19 or newer:

    + for VP4630 and VP4650

        ```bash
        ./build.sh vp4630_vp4650
        ```

    + for VP4670

        ```bash
        ./build.sh vp4670
        ```

The resulting coreboot image will be placed in the coreboot directory as
`protectli_vault_cml_<version>_vp4630_vp4650.rom` or
`protectli_vault_cml_<version>_vp4670.rom` respectvely.
