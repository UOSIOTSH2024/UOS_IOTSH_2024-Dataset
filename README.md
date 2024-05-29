The UOS_IOTSH_2024 Dataset
This is a dataset built with network traffic collected from RPL-based IoT networks under different Sinkhole Attack scenarios that have been simulated using the COOJA simulator.

Attack Scenario
The UOS_IOTSH_2024 Dataset simulates an attack scenario where an intruder infiltrates a node already integrated into a functioning RPL-based IoT network to execute a sinkhole attack. An adversary leverages the compromised node's established network privileges to orchestrate malicious activities. By compromising an existing node within the network, the attacker gains the ability to covertly manipulate the network's communication dynamics, directing traffic flow in a manner that disrupts normal operations and compromises network integrity. Once the intruder has gained access to the victim node, it modifies the rank information advertised by the compromised node, falsely advertising an optimal path to the root node. The attacker attracts traffic towards the compromised node, effectively hijacking the network's communication pathways.

Composition of the UOS_IOTSH_2024 Dataset
The UOS_IOTSH_2024 dataset was created with the following main categories:
- Traffic from RPL-based IoT networks operating normally under multiple scenarios:
-- A small network with a single DODAG.
-- A medium-sized network with a single DODAG.
-- A medium-sized network with dual DODAGs.

- Traffic from RPL-based IoT networks under a single sinkhole attack:
-- A small network with a single DODAG (multiple instances for different attacker locations)
-- A medium-sized network with a single DODAG (multiple instances for different attacker locations)
-- A medium-sized network with dual DODAGs (multiple instances for different attacker locations)

- Traffic from RPL-based IoT networks under dual sinkhole attacks:
-- A small network with a single DODAG (multiple instances for different attacker locations)
-- A medium-sized network with a single DODAG (multiple instances for different attacker locations)
-- A medium-sized network with dual DODAGs (multiple instances for different attacker locations)

Features Included in the UOS_IOTSH_2024 Dataset
The dataset was first created with the 6 features shown below extracted directly from the raw network traffic collected from the COOJA simulations:
- Source and Destination IDs (IPv6 addresses of the source and destination nodes). These are used to identify child and parent nodes which are affected by the sinkhole attack
- Node Rank (Relative position of node relative to other nodes with respect to a DODAG root). This is the exact attack target of sinkhole attack.
- Message Length field - The length of the RPL control message (64: DIS, 97 or 102: DIO, 76: DAO or 5: DAO ACK)
- Info field which indicates the type of the RPL control message.
- Protocol field - The communication protocol (ICMPV6, IEEE802.1 or UDP).

Procedure for Simulating the Attack using the COOJA Simulator
Simulating the internal sinkhole attack proceeded according to the following steps:
- After the network is constructed in COOJA, it will be allowed to run normally for about 100 seconds until the DODAG is constructed successfully and the network starts to transmit UDP data packets. 
- After the conclusion of the 100 seconds, a designated node alters its behavior and launches the sinkhole attack by broadcasting DIO messages that falsely advertise a rank very close to that of the root node.
- The network is allowed to operate normally for another 100 seconds until the DODAG re-construction process completes.
- After the conclusion of the 4 minutes, Wireshark will be used to collect all of the exchanged packets throughout the simulation time. These packets will be recorded in the Dataset, with their exact sequencing preserved.

Collection of Normal Network Traffic for the UOS_IOTSH_2024 Dataset
A number of network configurations were built in COOJA and allowed to operate normally to establish the baseline normal behavior for the simulated networks:
- A network comprised of a single router (representing the root node) and 12 Tmote Sky Mote nodes (representing the sensor nodes) was constructed in the COOJA simulator. The sensor nodes were arranged in rows with varying distances from the root to encourage a hierarchical DODAG. To prevent potential data bias, the placement of nodes with respect to their node IDs was deliberately randomized.
- A medium-sized network comprised of a single root node and 24 Tmote Sky Mote nodes was constructed in COOJA. The sensor nodes were distributed in a manner similar to the previous network to encourage a hierarchical construction of the DODAG. Then, the same steps were followed for collecting the network traffic from the COOJA simulator. 
- A medium-sized network comprised of two routers (representing two root nodes) and 24 Tmote Sky Mote nodes was built in COOJA. The nodes were distributed in a manner to encourage the establishment of two DODAGs.
 
Collection of Traffic from Networks Subjected to a Single Attacker
The same three combinations of network sizes and structures from the previous section were subjected to a single sinkhole attack to enable the extraction of representative traffic from networks under attack.
- The small single-DODAG Network was recreated, then attacks using different nodes within the network were simulated to extract the data samples. An exhaustive set of simulations were conducted where a different node was selected as the compromised node for each iteration.
- The medium-sized single-DODAG network was exhaustively simulated with attacks originating from a different location for each iteration. 
- The dual-DODAG network was recreated and simulated with an attack being launched using one of the border nodes after 100 seconds of simulation time. The simulation was repeated exhaustively for each of the border nodes.

Collection of Traffic from Networks Subjected to Dual Attackers
- The small single-DODAG network was recreated and simulated with two nodes launching sinkhole attacks. The following representative combinations were used to collect the data for the datatset: One attacker at L2 and another attacker at L3: Node 8 and Node 2, One attacker at L2 and another attacker at L3: Node 11 and Node 12, One attacker at L2 and another attacker at L4: Node 5 and Node 9, and One attacker at L3 and another attacker at L4: Node 5 and Node 12.
- The medium-sized single-DODAG network was recreated and simulated with two nodes launching attacks with a 50 second interval.
- The medium-sized Dual-DODAG network was recreated and simulated with two nodes launching a sinkhole attack. The dataset included situations where each attacker is in a separate DODAG. 

Complete composition of the UOS_IOTSH_2024 Dataset
Once the samples for all of the different scenarios were collected, we ended up with a dataset comprised of 9 different categories covering different network sizes, different network topologies, and different attacker counts. In total, the dataset covers 78 different attack scenarios, and includes 1,771,880 samples of exchanged messages.
