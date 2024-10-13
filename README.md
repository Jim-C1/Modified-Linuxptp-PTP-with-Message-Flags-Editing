# Modified_Linuxptp_with_PTP_Message_Flags Editing

## Modifications by Jim C
**Date**:  13.Oct.2024  

**Summary**: This project is based on linuxptp 3.1.1. We have made the following changes:
- Added 'FlagField' flags to the following PTP messages:
  1. Pdelay request
  2. Pdelay response
  3. Follow-up
  4. Sync
  5. Pdelay response follow-up
- All code changes are located in the `port.c` file.

## Disclaimer
This project is intended for demonstration purposes only and is not suitable for production environments.

## Getting the Modified Version
This repository contains modifications to the original linuxptp project, version 3.1.1. You can down the modified version with the changes mentioned above on this github page.

## Future Plan
We plan to update this project with more detailed information about the changes and the reasoning behind them in the near future.

## The original project
For details on the original project, please refer to the information below.


* Introduction

  This software is an implementation of the Precision Time Protocol
  (PTP) according to IEEE standard 1588 for Linux. The dual design
  goals are to provide a robust implementation of the standard and to
  use the most relevant and modern Application Programming Interfaces
  (API) offered by the Linux kernel. Supporting legacy APIs and other
  platforms is not a goal.

* License

  The software is copyrighted by the authors and is licensed under the
  GNU General Public License. See the file, COPYING, for details of
  the license terms.

* Features

  - Supports hardware and software time stamping via the Linux
    SO_TIMESTAMPING socket option.

  - Supports the Linux PTP Hardware Clock (PHC) subsystem by using the
    clock_gettime family of calls, including the clock_adjtimex system
    call.

  - Implements Boundary Clock (BC), Ordinary Clock (OC) and
    Transparent Clock (TC).

  - Transport over UDP/IPv4, UDP/IPv6, and raw Ethernet (Layer 2).

  - Supports IEEE 802.1AS-2011 in the role of end station.

  - Modular design allowing painless addition of new transports and
    clock servos.

  - Implements unicast operation.

  - Supports a number of profiles, including:

    - The automotive profile

    - The default 1588 profile.

    - The enterprise profile.

    - The telecom profiles G.8265.1, G.8275.1, and G.8275.2.

  - Supports the NetSync Monitor protocol.

  - Implements Peer to peer one-step.

  - Supports bonded, IPoIB, and vlan interfaces.


* Getting the Original Source Code

  If you are looking for the original linuxptp source code, use the following instructions:

  The original project source code is managed using the git version control system. 
  To get your own copy of the original linuxptp project sources, use the following command:


#+BEGIN_EXAMPLE
  git clone git://git.code.sf.net/p/linuxptp/code linuxptp
#+END_EXAMPLE

  If the git protocol is blocked by your local area network, then you 
can use the alternative HTTP protocol instead:


#+BEGIN_EXAMPLE
  git clone http://git.code.sf.net/p/linuxptp/code linuxptp
#+END_EXAMPLE

* System Requirements

  In order to run this software, you need Linux kernel version 3.0 or
  newer.  Check whether your network interface supports PTP with the
  following command.

#+BEGIN_EXAMPLE
  ethtool -T eth0
#+END_EXAMPLE

  This command shows whether a MAC supports hardware or software time
  stamping.  The following example output indicates support for
  hardware time stamping.

#+BEGIN_EXAMPLE
Time stamping parameters for eth6:
Capabilities:
        hardware-transmit     (SOF_TIMESTAMPING_TX_HARDWARE)
        software-transmit     (SOF_TIMESTAMPING_TX_SOFTWARE)
        hardware-receive      (SOF_TIMESTAMPING_RX_HARDWARE)
        software-receive      (SOF_TIMESTAMPING_RX_SOFTWARE)
        software-system-clock (SOF_TIMESTAMPING_SOFTWARE)
        hardware-raw-clock    (SOF_TIMESTAMPING_RAW_HARDWARE)
PTP Hardware Clock: 1
Hardware Transmit Timestamp Modes:
        off                   (HWTSTAMP_TX_OFF)
        on                    (HWTSTAMP_TX_ON)
Hardware Receive Filter Modes:
        none                  (HWTSTAMP_FILTER_NONE)
        all                   (HWTSTAMP_FILTER_ALL)
#+END_EXAMPLE

  The next example shows the case where the MAC only supports software
  time stamping.  The ~ptp4l~ program requires either the ~-S~ command
  line argument or the ~time_stamping software~ configuration option
  when using such interfaces.

#+BEGIN_EXAMPLE
Time stamping parameters for enp6s0:
Capabilities:
        software-transmit     (SOF_TIMESTAMPING_TX_SOFTWARE)
        software-receive      (SOF_TIMESTAMPING_RX_SOFTWARE)
        software-system-clock (SOF_TIMESTAMPING_SOFTWARE)
PTP Hardware Clock: none
Hardware Transmit Timestamp Modes: none
Hardware Receive Filter Modes: none
#+END_EXAMPLE

  Note the ~software-transmit (SOF_TIMESTAMPING_TX_SOFTWARE)~
  capability.  If this is lacking, then the MAC cannot be used at
  all.  However, adding this capability entails adding a single line
  of code to the device driver.

* Installation

   1. Just type 'make'

   2. If you compiled your own kernel (and the headers are not
      installed into the system path), then you should set the
      KBUILD_OUTPUT environment variable as in the example, above.

   3. In order to install the programs and man pages into /usr/local,
      run the 'make install' target. You can change the installation
      directories by setttings the variables prefix, sbindir, mandir,
      and man8dir on the make command line.

* Getting Involved

  The software development is hosted at Source Forge.

  https://sourceforge.net/projects/linuxptp/

** Reporting Bugs

   Please report any bugs or other issues with the software to the
   linuxptp-users mailing list.

   https://lists.sourceforge.net/lists/listinfo/linuxptp-users

** Development

   If you would like to get involved in improving the software, please
   join the linuxptp-devel mailing list.

   https://lists.sourceforge.net/lists/listinfo/linuxptp-devel

*** Submitting Patches

   1. Before submitting patches, please make sure that you are starting
      your work on the *current HEAD* of the git repository.

   2. Please checkout the ~CODING_STYLE.org~ file for guidelines on how to
      properly format your code.

   3. Describe your changes. Each patch will be reviewed, and the reviewers
      need to understand why you did what you did.

   4. *Sign-Off* each commit, so the changes can be properly attributed to
      you and you explicitely give your agreement for distribution under
      linuxptp's license. Signing-off is as simple as:

      #+BEGIN_EXAMPLE
      git commit -s
      #+END_EXAMPLE

      or by adding the following line (replace your real name and email)
      to your patch:

      #+BEGIN_EXAMPLE
      Signed-off-by: Random J Developer <random@developer.example.org>
      #+END_EXAMPLE

   5. Finally, send your patches via email to the linuxptp-devel mailing
      list, where they will be reviewed, and eventually be included in the
      official code base.

      #+BEGIN_EXAMPLE
      git send-email --to linuxptp-devel@lists.sourceforge.net origin/master
      #+END_EXAMPLE


* Original Project Sponsors and Contributors

  The following section details contributions and acknowledgments from the original linuxptp project:


* Thanks

  Thanks to AudioScience Inc for sponsoring the 8021.AS support.

  - http://www.audioscience.com

  Thanks to Exablaze for donating an ExaNIC X10

  - http://exablaze.com/exanic-x10

  Thanks to Intel Corporation for donating four NICs, the 82574,
  82580, 82599, and the i210.

  - http://www.intel.com
  - http://e1000.sourceforge.net

  Thanks to Meinberg Funkuhren for donating a LANTIME M1000.

  - https://www.meinbergglobal.com

  Thanks to Moser Baer for sponsoring the Telecom Profiles and unicast
  support.

  - http://www.mobatime.com

  For testing I use an OTMC 100 grandmaster clock donated by OMICRON Lab.

  - http://www.omicron-lab.com/ptp
