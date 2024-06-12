TWRP device tree for LG V40 ThinQ

The LG V40 ThinQ (codenamed _"judypn"_) is a high-end smartphone from LG.
LG V40 was announced and released in October 2018.

## Device specifications

| Baisc                   | Specification Sheet                                                                                                                |
| ----------------------: |:---------------------------------------------------------------------------------------------------------------------------------- |
| SoC                     | Qualcomm SDM845 Snapdragon 845                                                                                                     |
| CPU                     | Octa-core (4x2.8 GHz Kryo 385 Gold & 4x1.8 GHz Kryo 385 Silver)                                                                    |
| GPU                     | Adreno 630                                                                                                                         |
| Memory                  | 6GB (LPDDR4X)                                                                                                                      |
| Shipped Android Version | 8.1 with LGUX                                                                                                                      |
| Last version of Android | 10.0 with LGUX                                                                                                                     |
| Storage                 | 64/128 UFS2.1                                                                                                                      |
| Battery                 | Non-removable Li-Poly 3300 mAh battery                                                                                             |
| Display                 | 1440 x 3120 pixels, 19.5:9 ratio, 6.4 inches, P-OLED, HDR10 (~537 ppi density)                                                     |
| Extras                  | IP68, NFC                                                                                                                          |

## Device picture

![LG V40](https://cdn.kalvo.com/uploads/img/gallery/lg-v40-thinq-1.jpg)


## Kernel

Prebuilt kernel source:
https://github.com/EmanuelCN/android_kernel_lge_sdm845/tree/recovery

## Compile

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
  <project name="EAZYBLACK/recovery_device_lge_judy" path="device/lge/judypn" remote="github" revision="judypn"/>
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
lunch twrp_judypn-eng
make adbd bootimage
```
