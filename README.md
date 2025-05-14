# ION-DTN + CORE 3-Node Chat Simulation

This repository documents and demonstrates a 3-node Delay Tolerant Network (DTN) chat setup using NASA's ION-DTN and the CORE network emulator. Messages are sent using the Bundle Protocol over LTP/UDP to simulate resilient communications in high-delay or disconnected conditions. This project was developed as a computer science capstone under Dr. Ronny L. Bull. While it is scalable to multiple nodes, this implementation demonstrates the architecture using a 3-node scenario.

The lab workstation was running Ubuntu 24.04 at the time of installation and testing.

# Installing ION on Ubuntu

Update packages:
```
sudo apt update
```

Install dependencies:
```
sudo apt install automake autoconf libtool m4 gcc make
```

Clone the ION-DTN repo from GitHub:
```
git clone https://github.com/nasa-jpl/ION-DTN.git
```

Change directory into ION-DTN:
```
cd ION-DTN/
```

Run configure (with the old semaphorese flag):
```
autoreconf -fi
./configure --enable-force-svr4-semaphores
```

Compile make:
```
make
sudo make install
```

Run ldconfig (first letter is a lowercase L):
```
sudo ldconfig
```

# Installing CORE on Ubuntu

Update and install dependencies:
```
sudo apt update
sudo apt install -y core-network core-gui
```
> This installs:
- `core-daemon`: the backend
- `core-gui`: the GUI

Run the CORE GUI:
```
sudo core-gui
```

# Configuring CORE

The scenario for this simulation involved a router connected to a switch, which was then connected to three nodes.

When the scenario is active, double-click on the nodes
Let X be a node num:
```
root@nX
```

su over to an admin profile:
```
su <profile_name>
```

Remove any old ion_node file(s):
```
rm /tmp/ion_nodes
```

DEFINE environmental variable:
```
export ION_NODE_LIST_DIR=/tmp
```

Copy over runcontrol + ionconfig files 
Within the file directory, let X be a CORE host num:
```
cp host20.rc /tmp/pycore.1/nX.conf/
cp host20.ionconfig /tmp/pycore.1/nX.conf/
```

Run ION scenarios
Let X be a host num:
```
ionstart -I hostX.rc
```

Start node communication
Let X be a host num:
```
bpchat ipn:X.1 ipn:X.1 ipn:X.1
```

# References
`Special thanks to David Cook for debugging and installation :catdance:`
- ION-DTN Github: [https://github.com/nasa-jpl/ION-DTN](https://github.com/nasa-jpl/ION-DTN)
- ION-DTN Official Documentation: [https://nasa-jpl.github.io/ION-DTN/](https://nasa-jpl.github.io/ION-DTN/)
- CORE Emulator: [https://github.com/coreemu/core](https://github.com/coreemu/core)
- *DTN architecture: RFC 4838, RFC 5050*

> NASA’s Interplanetary Overlay Network (ION-DTN) is an open-source Delay/Disruption Tolerant Networking (DTN) implementation developed by the Jet Propulsion Laboratory.
- © 2004-2024 United States Government as represented by the Administrator of the National Aeronautics and Space Administration. All Rights Reserved.
- Licensed under the NASA Open Source Agreement.

> CORE is a network emulation platform originally developed by Boeing and now maintained as an open-source project for academic and research use.
- Originally developed by Boeing Research and Technology.
- Licensed under the BSD-2-Clause license.
