PeerStreamer on OpenWRT
=================================================================

This guide describes how to build PeerStreamer for OpenWRT.

# OpenWRT cross-compilation toolchain

In order to build PeerStreamer for OpenWRT you need a properly configured
OpenWRT cross-compilation toolchain. We report in this guide the basic steps for
setting it up but for up-to-date instructions refer to the official
[OpenWrt build system documentation](https://wiki.openwrt.org/doc/howto/build).

This guide has been tested on Ubuntu 16.04 LTS and in what follows we assume
Atheros AR7xxx/AR9xxx as the target platform for cross-compilation. If you
intend to cross-compile PeerStreamer for a different target you will need to
adapt the instructions reported below for using the correct cross-compilation
toolchain.

As a first step, install the required tools and libraries:

```bash
sudo apt-get install git-core build-essential libssl-dev libncurses5-dev unzip gawk subversion mercurial autotools-dev autoconf
```

Check out the OpenWRT source code:

```bash
git clone https://github.com/openwrt/openwrt.git
```

this creates a directory 'openwrt', which is the OpenWrt build system
build-directory. Let's suppose the full path to this directory is
'~/workspace/openwrt' and let's export the varialbe OPENWRT pointing to this
directory:

```bash
OPENWRT=~/workspace/openwrt
export OPENWRT
```
Update OpenWRT feeds:

```bash
cd ${OPENWRT}
./scripts/feeds update -a
```

Now it's time to configure the cross-compilation target and build OpenWRT. Start
the OpenWrt build system configuration interface by issuing the following
command:

```bash
make menuconfig
```

and select "Atheros AR7xxx/AR9xxx" as Target and "Generic" as Subtarget.
Everything is now ready for building the image(s), which is done with one single
command:

```bash
make
```

Once the build process completes the cross-compilation toolchain will be
available in directory
${OPENWRT}/staging_dir/toolchain-mips_34kc_gcc-5.3.0_musl-1.1.15/ (the exact gcc
and musl versions depends on the OpenWRT version used. The ones reported in the
example refer to OpenWRT 15.05.1).

Now export a few variables that will help us during the PeerStreamer build
process:

```bash
OPENWRTXTOOLS=${OPENWRT}/staging_dir/toolchain-mips_34kc_gcc-5.3.0_musl-1.1.15/
export OPENWRTXTOOLS
OPENWRTXTOOLSBIN=${OPENWRTXTOOLS}/bin/
export OPENWRTXTOOLSBIN
PATH=$PATH:$OPENWRTXTOOLSBIN
export PATH
STAGING_DIR=${OPENWRTXTOOLS}
export STAGING_DIR
```

# Build PeerStreamer

For building PeerStreamer using the OpenWRT toolchain execute the following
commands:

```bash
cd ~/workspace
git clone https://github.com/netCommonsEU/PeerStreamer-build.git
cd PeerStreamer-build
make prepare
make ml HOSTARCH=mips-openwrt-linux
```

The executable will be located in
"~/workspace/PeerStreamer-build/Streamers/streamer-ml-grapes-static. Just copy
it on your device running OpenWRT for using it.
