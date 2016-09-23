This is a BETA Snap
===================

The Snap is based on Quagga Version 1.0.20160315 with some modifications
to get Snaps working.

Using the Quagga Snap
=====================

After installing the Snap, the priviledged plug need to be connected:

    snap connect quagga:network-control ubuntu-core:network-control

Enabling/Disabling Quagga Daemons
---------------------------------

By default (at this time), all Quagga daemons will be enabled on 
installation. If you want to disable a specific daemon, then use 
the systemctl commands

ie for `ospf6d` (OSPFv3):

    systemctl disable snap.quagga.ospf6d.service
    systemctl enable snap.quagga.ospf6d.service

The daemons are: `ripd`, `ripngd`, `ospfd`, `ospf6d`, `isisd`, `bgpd`, 
`pimd`, `zebra`

Commands defined by this snap
-----------------------------

- `quagga.vtysh`:
	Quagga VTY Shell (configuration tool)
- `quagga.version`:
	Returns output of `zebra --version` to display version and configured 
	options
- `quagga.readme`:
	Returns this document `cat README_usage.md`

and for debugging defined at this time (May get removed later - do not 
depend on them). These are mainly intended to debug the Snap

- `quagga.zebra-debug`:
	Starts zebra daemon in foreground
- `quagga.ripd-debug`:
	Starts ripd daemon in foreground
- `quagga.ripngd-debug`:
	Starts ripng daemon in foreground
- `quagga.ospfd-debug`:
	Starts ospfd daemon in foreground
- `quagga.ospf6d-debug`:
	Starts ospf6d daemon in foreground
- `quagga.isisd-debug`:
	Starts isisd daemon in foreground
- `quagga.bgpd-debug`:
	Starts bgpd daemon in foreground
- `quagga.pimd-debug`:
	Starts pimd daemon in foreground

FAQ
---
- quagga.vtysh displays `--MORE--` on long output. How to suppress this?
    - Define `VTYSH_PAGER` to `cat` (default is `more`). (Ie add 
      `export VTYSH_PAGER=cat` to the end of your `.profile`)

Sourcecode available
====================

The source for this SNAP is available at

    https://git.netdef.org/scm/osr/quagga-snap.git

in the `feature/snap` branch. Please be aware that this location may
change in one of the next version.

Instructions for rebuilding the snap are at

    https://git.netdef.org/projects/OSR/repos/quagga-snap/browse/snapcraft/README.snap_build.md

Feedback welcome
================

Please send Feedback about this snap to Martin Winter at 
`mwinter@opensourcerouting.org`

