# Kernel Toolchains 
# Snapdragon clang version 8.0.6
--------
### Install latest version of Make from [**Here**](https://ftp.gnu.org/gnu/make).
### These toolchains are only for Linux machines, don't messup with it in Windows.
--------
Getting Started
==================================================
--------
### How to use these toolchains for compiling android Kernels ?
--------
1. Clone this toolchain repo in tools folder
```bash
$ git clone --depth=1 https://github.com/pkm774/android-kernel-tools tools
```
-> Now compile using AOSP clang or Snapdragon clang.
2. Install required packages
```bash
$ sudo apt-get update && sudo apt-get upgrade -y
$ sudo apt-get install -y gcc-aarch64-linux-gnu
```
3. Set path for the toolchain.

```bash
	PATH="$TOP/tools/sdclang/linux-x86_64/bin:$PATH"
```

4. Commands for compiling with **Snapdragon clang**.

```bash
$ 	make \
	     clean \
	     mrproper \
	     O=out \
	     ARCH=arm64 \
	     SUBARCH=ARM64 \
	     CC=clang \
    	     CROSS_COMPILE=aarch64-linux-gnu- \
    	     CROSS_COMPILE_ARM32=arm-linux-gnueabi- \
	     ${DEVICE}_defconfig
    
$	make \
	     O=out \
	     ARCH=arm64 \
	     SUBARCH=ARM64 \
	     CC=clang \
    	     CROSS_COMPILE=aarch64-linux-gnu- \
    	     CROSS_COMPILE_ARM32=arm-linux-gnueabi- \
	     -j$(nproc --all)
```
--------
## NOTES:
$ {DEVICE}_defconfig is the kernel config file used to compile kernel.
Kernel binaries are produced in **out** directory.

--------
##### Snapdragon clang is taken from : [**developer.qualcomm.com**](https://developer.qualcomm.com/forums/software/snapdragon-llvm-compiler-android)
##### Give a star if you liked my work :)
