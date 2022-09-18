# TWRP Device configuration for Motorola Moto G30

## Device specification

Basic   | Spec Sheet
-------:|:------------------------
CPU     | Octa-core (4x2.0 GHz Kryo 260 Gold & 4x1.8 GHz Kryo 260 Silver)
CHIPSET | Qualcomm SDM662 (SM6115 "Bengal") Snapdragon 662
GPU     | Adreno 610
Memory  | 4GB, 6GB
Shipped Android Version | 11.0
Storage | 64GB, 128GB
Battery | 5000 mAh
Dimensions | 165.2 x 75.7 x 9.1 mm (6.50 x 2.98 x 0.36 in)
Display | IPS LCD, 90Hz, 720 x 1600 pixels, 20:9 ratio (~269 ppi density)
Rear Camera 1 | 64 MP, f/1.7, 26mm (wide), 1/1.97", 0.7µm, PDAF
Rear Camera 2 | 8 MP, f/2.2, 118˚ (ultrawide), 1/4.0", 1.12µm
Rear Camera 3 | 2 MP, f/2.4, (macro)
Rear Camera 4 | 2 MP, f/2.4, (depth)
Front Camera | 13 MP, f/2.2, (wide), 1/3.1", 1.12µm

![Device Picture](https://fdn2.gsmarena.com/vv/bigpic/motorola-moto-g30.jpg)


### Kernel Source
From Stock ROM user-12-S0RCS32.41-10-9-2-4-7b23e3-release-keys


### How to compile
First repo init the twrp-11 tree (and necessary qcom dependencies):

```
mkdir ~/android/twrp-11
cd ~/android/twrp-11
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-11
mkdir -p .repo/local_manifests
curl https://raw.githubusercontent.com/TeamWin/buildtree_manifests/master/min-aosp-11/qcom.xml > .repo/local_manifests/qcom.xml
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_motorola_caprip" path="device/motorola/caprip" remote="TeamWin" revision="android-11"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/4964

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_caprip-eng
make adbd bootimage
```
