Building your own Quagga Snap
=============================
(Tested on Ubuntu 16.04 with Snap Version 2, does not work on Ubunut 15.x
which uses earlier versions of snaps)

1. Install snapcraft:

        sudo apt-get install snapcraft
	
2. Checkout Quagga under a **unpriviledged** user account

    _At this time, a special modified version of Quagga is required, so 
    please download from URL given below_

        git clone https://git.netdef.org/scm/osr/quagga-snap.git quagga
        cd quagga
        git checkout feature/snap

3. Run Bootstrap and make distribution tar.gz

        ./bootstrap.sh
        ./configure --with-pkg-extra-version=-MySnapVersion
        make dist
			
    Note: configure parameters are not important for the Snap building 
    - except the `with-pkg-extra-version` if you want to give the Snap 
    a specific name to mark your own unoffical build

    This will build `quagga-something.tar.gz` - the distribution tar and 
    the snapcraft/snapcraft.yaml with the matching version number

4. Create snap

        cd snapcraft
        snapcraft

    You should now end up with `quagga_something.snap`

Installing the snap 
===================
(This can be done on a different system)

1. Install snapd

        sudo apt-get install snapd

2. Install self-built quagga snap

        snap install ./quagga*.snap

    Connect the priviledged `network-control` plug to the snap:

        snap connect quagga:network-control ubuntu-core:network-control

DONE.

The Snap will be auto-started and running. 

Operations
==========

### Quagga Daemons
At this time, all Quagga daemons are auto-started.

A daemon can be stopped/started with (ie ospf6d)

    systemctl stop snap.quagga.ospf6d.service
    systemctl start snap.quagga.ospf6d.service

or disabled/enabled with

    systemctl disable snap.quagga.ospf6d.service
    systemctl enable snap.quagga.ospf6d.service

### Quagga Commands
All the commands are prefixed with quagga.

    quagga.vtysh       -> vtysh
    quagga.version     -> Just gives version output (zebra --version)
    quagga.readme      -> Returns simple README with hints on using Quagga

    quagga.bgpd-debug  -> Directly start each daemon (without service)
    quagga.isisd-debug
    quagga.ospf6d-debug
    quagga.ospfd-debug
    quagga.pimd-debug
    quagga.ripd-debug
    quagga.ripngd-debug
    quagga.zebra-debug

vtysh can be accessed as quagga.vtysh (Make sure you have /snap/bin in your
path). If access as `vtysh` instead of `quagga.vtysh` is needed, a symlink 
can be created:

    sudo ln -s /snap/bin/quagga.vtysh /usr/local/bin/vtysh

