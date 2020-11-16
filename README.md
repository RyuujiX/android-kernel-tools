# Kernel Toolchains 
# AOSP (GCC & Clang ) and Qualcomm Snapdragon Clang
--------
How to compile android kernel? Detailed Instructions [**Here**](https://forum.xda-developers.com/t/reference-how-to-compile-an-android-kernel.3627297/).
Install latest version of Make from [**Here**](https://ftp.gnu.org/gnu/make).
**Instructions here are only for Linux OS machines, don't get messed in Windows unless you know how to use properly.**
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

## For using AOSP clang:
2. Set path for the toolchains.

```bash
$	PATH="tools/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin:$PATH"
$	PATH="tools/gcc/linux-x86/arm/arm-linux-androideabi-4.9/bin:$PATH"
$	PATH="tools/clang/host/linux-x86/clang-r399163b/bin:$PATH"
$	export LD_LIBRARY_PATH="tools/clang/host/linux-x86/clang-r399163b/lib64:$LD_LIBRARY_PATH"
```
3. Export required flags

```bash
$	export ARCH=arm64
$	export SUBARCH=ARM64
$	export CLANG_TRIPLE=aarch64-linux-gnu-
$	export CROSS_COMPILE=aarch64-linux-android-
$	export CROSS_COMPILE_ARM32=arm-linux-androideabi-
```
>> ARCH & SUBARCH according to your device.

4. Use these command for compiling with **AOSP clang**.

```bash
$ make \
	O=out \
	clean \
	mrproper \
	CC=clang \
	AR=llvm-ar \
	NM=llvm-nm \
	LD=ld.lld \
	STRIP=llvm-strip \
	OBJDUMP=llvm-objdump \
	OBJCOPY=llvm-objcopy \
	${DEVICE}_defconfig
  
$ make \
	O=out \
	clean \
	mrproper \
	CC=clang \
	AR=llvm-ar \
	NM=llvm-nm \
	LD=ld.lld \
	STRIP=llvm-strip \
	OBJDUMP=llvm-objdump \
	OBJCOPY=llvm-objcopy \
	-j$(nproc --all)
```

## For using Snapdragon clang:

* Install gcc-aarch64-linux-gnu in Your machine. For Ubuntu:
```bash
$ sudo apt-get update && sudo apt-get upgrade -y
$ sudo apt-get install -y gcc-aarch64-linux-gnu
```
2. Set path for the toolchain.

```bash
$	PATH="$TOP/tools/sdclang/linux-x86_64/bin:$PATH"
```
3. Export required flags.

```bash
$	export ARCH=arm64
$	export SUBARCH=ARM64
$	export CROSS_COMPILE=aarch64-linux-gnu-
$	export CROSS_COMPILE_ARM32=arm-linux-gnueabi-
```
>> ARCH & SUBARCH according to your device.

4. Use these command for compiling with **Snapdragon clang**.

```bash
$ make \
	O=out \
	clean \
	mrproper \    
	CC=clang \
	${DEVICE}_defconfig
    
$ make \
	O=out \    
	CC=clang \
	-j$(nproc --all)
```
--------
## NOTES:
-> $ {DEVICE}_defconfig is the kernel config file used to compile kernel. Kernel binaries are produced in **out** directory.

#### # It will be easy to compile kernel with a bash script. Make a bash script in kernel folder and set toolchain path according to your folders.
--------
##### AOSP clang is taken from : [**Android Open Source Project**](https://source.android.com)
##### Snapdragon clang is taken from : [**developer.qualcomm.com**](https://developer.qualcomm.com/forums/software/snapdragon-llvm-compiler-android)
##### Give a star if you liked my work :)
