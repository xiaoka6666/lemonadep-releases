Copyright (C) 2025
# 如何为 OnePlus 9 Pro 编译 Android 15 ROM (以 crDroid 为例)

## 准备环境
- 最低配置 16G 物理内存 + 设置至少 32G SWAP ，至少 350G 空闲 SSD 容量，CPU 无要求
- 环境搭建依赖安装参考 lineage wiki 如 https://wiki.lineageos.org/devices/rosemary/build/variant1/ [Ubuntu/debian系]  
- Fedora/redhat系依赖安装参考 https://gist.github.com/axxx007xxxz/60fea50f4b123e0163f972d1709068c2 或 https://github.com/tripLr/Fedora-Server-Tools/blob/master/fedora_setup_aosp.sh  
- Arch Linux 用户参考 archlinux wiki: https://wiki.archlinux.org/title/Android#Building

## 如何编译
1. 拉源码/Pull source code
- ROM:
```
mkdir ~/android/crDroid && cd ~/android/crDroid
```
```
repo init -u https://github.com/crdroidandroid/android.git -b 15.0 --git-lfs --depth=1
```
```
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```
- lemonadep:  
```
git clone https://github.com/xiaoka6666/android_device_oneplus_lemonadep -b lineage-22.2 --single-branch --depth=1 device/oneplus/lemonadep
git clone https://github.com/xiaoka6666/android_device_oneplus_sm8350-common -b lineage-22.2 --single-branch --depth=1 device/oneplus/sm8350-common
git clone https://github.com/xiaoka6666/android_kernel_oneplus_sm8350 -b lineage-22.2 --single-branch --depth=1 kernel/oneplus/sm8350
git clone https://github.com/xiaoka6666/android_hardware_oplus -b lineage-22.2 --single-branch --depth=1 hardware/oplus
```
2.提取专有 blob
```
./extract-files.py
```

3. 初始化环境和开始编译
```
source build/envsetup.sh
```
```
breakfast lemonadep
```
```
croot
brunch lemonadep
```
