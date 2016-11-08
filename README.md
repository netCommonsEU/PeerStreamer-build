PeerStreamer build system
===========================

This is the PeerStreamer build system that automatizes the build and installation
process of PeerStreamer.

For the moment perform all the operations using the D3.2-testing branch:

`git clone -b D3.2-testing
https://github.com/netCommonsEU/PeerStreamer-build.git`

## Requirements

The following has been tested on Ubuntu 16.04 LTS but any Linux distribution with
proper developing tools installed should work.

On ubuntu execute the following command for installing the tools required for
building and testing PeerStreamer:

`sudo apt-get install build-essential libssl-dev libncurses5-dev unzip gawk
autoconf gstreamer1.0-plugins-base gstreamer1.0-plugins-good
gstreamer1.0-plugins-bad ffmpeg vlc`

The build system handles all the libraries required by PeerStreamer (NAPA and
GRAPES) and PeerStreamer itself as git submodules.

## Build

Execute the following command for checking out the submodules:

`make prepare`

then execute the following command for starting the build process:

`make ml`

## Install

Use the following command for installing PeerStreamer (root permissions
required):

`make install`

the command will copy the executable in the directory /opt/peerstreamer/ and
will create a symbolic link pointing to the executable in
/usr/local/bin/peerstreamer.

For uninstalling PeerStreamer just execute:

`sudo make uninstall`

