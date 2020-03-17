This repository contains the sources of dvblast for OpenWrt, under the folder "sources".

In the foler "binaries" there are the precompiled and ready to execute binaries for le MIPS architecture.


To cross compile this program for you architecture for OpenWrt :

1) Get the sdk for your architecture : https://openwrt.org/docs/guide-developer/using_the_sdk

2) Execute these commands, replacing the necessary parts (you can find them by exploring the sdk folder)

export STAGING_DIR=place-here-the-directory-of-the-sdk/staging_dir/

export TOOLCHAIN_DIR=$STAGING_DIR/toolchain-architecture-_gcc-place-here-the-version-of-gcc-you-find-in-the-directory_musl/

export LDCFLAGS=$TOOLCHAIN_DIR/usr/lib

export LD_LIBRARY_PATH=$TOOLCHAIN_DIR/usr/lib

export PATH=$TOOLCHAIN_DIR/bin:$PATH

3) Go in the directory of the sources of this repository, and in the "libev-4.31" folder

4) Cross-compile the libev with these commands :

./configure --build=x86_64-linux-gnu (with architecture of your computer you can find in the list shown with "ls /usr/bin | grep gnu") -- host=mipsel-openwrt-linux (replace mipsel with the architecture of your OpenWrt router, and the SDK you downloaded)

make

5) Go in the ".libs" folder created and copy the files to /folder-of-the-SDK/staging_dir/toolchain-mipsel_24kc_gcc-8.3.0_musl/usr/lib

6) Delete "libev.so" and rename "libev.so.4.0.0" to "libev.so"

7) Go back in the sources folder of dvblast

8) Compile dvblast with this command :

make CC=folder-of-the-SDK/staging_dir/toolchain-architecture-to-change_gcc-number-to-change_musl/bin/architecture-openwrt-linux-gcc LD=folder-of-the-SDK/staging_dir/toolchain-architecture-to-change_gcc-number-to-change_musl/bin/architecture-openwrt-linux-ld

9) The "dvblast" and "dvblastctl" are the binaries for your architecture
