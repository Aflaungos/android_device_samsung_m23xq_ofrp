# OrangeFox Recovery Device configuration for Samsung Galaxy M23/F23 SM-M236B/SM-E236B (m23xq)

## Device specifications
Basic    | Spec Sheet
--------:|:----------------------
Chipset  | Qualcomm Snapdragon 750G
CPU      | Octa-core (6x1.8ghz Kryo 570 & 2x2.2ghz Cortex A77)
GPU      | Adreno 619
Memory   | 6GB RAM (LPDDR4X)
Storage  | 128GB
Shipped Android version | Android 12, OneUI 4.1
Battery  | Li-ion 5000mAh, non-removable
Display  | LCD, 120Hz, 525 nits, 6.6 inch, 1080 x 2408 pixels, 20:9 ratio

## Device picture
<img src="https://images.samsung.com/is/image/samsung/p6pim/br/sm-m236bzglzto/gallery/br-galaxy-m23-5g-sm-m236-422397-422397-sm-m236bzglzto-532669053?$1300_1038_PNG$" width="100%"/>

## Kernel Source
From Stock ROM
```
m23xqxx-user 14 UP1A.231005.007 M236BXXU5DWL1 release-keys
```

## Building
Generally, see https://wiki.orangefox.tech/en/dev/building

## How to compile
First repo init the twrp-12.1 tree:

```
mkdir ~/OrangeFox_sync
cd ~/OrangeFox_sync
git clone https://gitlab.com/OrangeFox/sync.git # (or, using ssh, "git clone git@gitlab.com:OrangeFox/sync.git")
cd ~/OrangeFox_sync/sync/
./orangefox_sync.sh --branch 12.1 --path ~/fox_12.1
mkdir -p .repo/local_manifests
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote name="me" 
        fetch="https://github.com/Aflaungos" />
  <project name="android_device_samsung_m23xq_ofrp" path="device/samsung/m23xq" remote="me" revision="ofrp_12.1"/>
</manifest>
```
Now you can sync your source:
```
repo sync
```
Finally execute these:
```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
lunch twrp_m23xq-eng
mka adbd recoveryimage
```
