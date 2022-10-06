# TWRP Device configuration for Motorola Moto G82 5G

## Device specification

Basic   | Spec Sheet
-------:|:------------------------
CPU     | Octa-core (2x2.2 GHz Kryo 660 Gold & 6x1.7 GHz Kryo 660 Silver)
CHIPSET | Qualcomm SM6375 Snapdragon 695 5G (6 nm)
GPU     | Adreno 619
Memory  | 6GB, 8GB
Shipped Android Version | 12
Storage | 128GB
Battery | 5000 mAh
Dimensions | 160.9 x 74.5 x 8 mm (6.33 x 2.93 x 0.31 in)
Display | AMOLED, 120Hz, 1080 x 2400 pixels, 20:9 ratio (~402 ppi density)
Rear Camera 1 | 50 MP, f/1.8 (wide), 1/2.76", 0.64µm, PDAF, OIS
Rear Camera 2 | 8 MP, f/2.2, 118˚ (ultrawide), 1/4.0", 1.12µm
Rear Camera 3 | 2 MP, f/2.4, (macro)
Front Camera | 16 MP, f/2.2, (wide), 1.0µm

![Device Picture](https://fdn2.gsmarena.com/vv/bigpic/motorola-moto-g82.jpg)


### Kernel Source
From Stock ROM RHODEP_RETAIL_12_S1SUS32.73-28-5-3


### How to compile
First repo init the twrp-12.1 tree:

```
mkdir ~/android/twrp-12.1
cd ~/android/twrp-12.1
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
mkdir -p .repo/local_manifests
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_motorola_rhodep" path="device/motorola/rhodep" remote="TeamWin" revision="android-12.1"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/5445

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_rhodep-eng
make adbd bootimage
```
