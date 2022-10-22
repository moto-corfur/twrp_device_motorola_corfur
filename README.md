# TWRP Device Tree for Motorola G71 5G (corfur).

## Setup repo tool
Setup repo tool from here https://source.android.com/setup/develop#installing-repo

## Compile

Sync TWRP manifest:

```
repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
```

Make a directory named local_manifest under .repo, and create a new manifest file, for example local_manifests.xml
and then paste the following

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote name="github"
	fetch="https://github.com/" />

<project path="device/motorola/corfur"
	name="moto-corfur/twrp_device_motorola_corfur"
	remote="github"
	revision="android-12.1" />
</manifest>
```
You might need to pick few patches from gerrit.twrp.me to get some stuff working.

Sync the sources with

```
repo sync -j$(nproc --all)
```

To build, execute this command:

```
. build/envsetup.sh; lunch twrp_corfur-eng; make bootimage
```

To test it:

```
# To temporarily boot it
fastboot boot out/target/product/corfur/boot.img 

# To make twrp replace stock recovery temporarily boot twrp and navigate
to advanced menu and select Flash Current TWRP option.
```

## Copyright

```
#
# Copyright (C) 2022 The Android Open Source Project
#
# SPDX-License-Identifier: Apache-2.0
#
