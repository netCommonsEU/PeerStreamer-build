PeerStreamer build system
===========================

This is the PeerStreamer build system that automatizes the build and installation
process of PeerStreamer.

For the moment perform all the operations using the D3.2-testing branch:

`git clone -b D3.2-testing
https://github.com/netCommonsEU/PeerStreamer-build.git`
`cd PeerStreamer-build`

## Requirements

The following has been tested on Ubuntu 16.04 LTS (x86_64) but any Linux
distribution with proper developing tools installed should work.

On ubuntu execute the following command for installing the tools required for
building and testing PeerStreamer:

```
sudo apt-get install git build-essential libssl-dev libncurses5-dev unzip gawk
autoconf gstreamer1.0-plugins-base gstreamer1.0-plugins-good
gstreamer1.0-plugins-bad ffmpeg vlc
```

The build system handles all the libraries required by PeerStreamer (NAPA and
GRAPES) and PeerStreamer itself as git submodules.

### Requirements for PeerViewer

The PeerStreamer build system can be used also for building and installing the
PeerStreamer web front-end [PeerViewer]
(https://github.com/netCommonsEU/PeerStreamer-peerviewer). For doing this you
need the development version of the glib2.0 and gstreamer1.0 libraries and a
properly configured Go and Node.js development environments.

On ubuntu you can execute the following command for installing the two required
libraries:

`sudo apt-get install libglib2.0-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev`

For configuring the Go development environment:

```
wget https://storage.googleapis.com/golang/go1.7.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.7.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin # Put this in ~/.profile to make it permanent
mkdir -p ~/go_workspace
export GOPATH=~/go_workspace/ # Put this in ~/.profile to make it permanent 
```

Refer to the [official Go documentation]
(https://golang.org/doc/install) for up-to-date instructions.

Finally, for configuring the Node.js development environment:

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install webpack -g
```

Refer to the [official Node.js documentation]
(https://nodejs.org/en/download/package-manager/) for up-to-date instructions.


## Build

Execute the following command for checking out the submodules:

`make prepare`

then execute the following command for building PeerStreamer (this will generate
the executable Streamers/peerstreamer:

`make ml`

and, finally, the following command if you want to compile also PeerViewer (this
will generate the executable PeerViewer/peerviewer):

```
make peerviewer
sudo -E make peerviewer_pack
```

## Install

Use the following command for installing PeerStreamer (and optionally PeerViewer
if it has been previously built):

`sudo make install`

the command will copy the executables in the directory /opt/peerstreamer/ and
will create a symbolic links pointing to the executables in
/usr/local/bin.

For uninstalling PeerStreamer and PeerViewer just execute:

`sudo make uninstall`

## Testing

For basic PeerStreamer/PeerViewer tests see the [testing instructions]
(https://github.com/netCommonsEU/PeerStreamer/blob/D3.2-testing/testing/Testing.md)
