# WDN-IoT-Dataset-Workbench

WDN refers to the collection of pipes, pumps, valves, junctions, tanks, and reservoirs.

![Alt text](dataset-network-epanet-src/NET_6_topology.png "WDN TOPOLOGY")

The considered network provides 4419 nodes, 3 reservoirs, and 5066 pipes. Each node is configured with a specific base demand pattern which represents the water request of the user during the whole simulation changing at a step size of an hour. 

In WDNs, base demand and satisfied water requests are two distinct concepts related to the amount of water needed and the amount of water that can be successfully supplied to the consumers.
In summary, while base demands represent the foreseen water consumption by users in a WDN, satisfied water request reflects the actual amount of water provided to them, taking into account the network's capacity and available resources and is labelled as demand value.

To create the dataset, we integrate the EPANET (US Environmental Protection Agency water NETwork) and the Water Network Tool for Resilience (WNTR). 
WNTR examines the geometric structure of the pipeline system along with a set of initial conditions (e.g. pipe roughness and diameter) and rules of how the system is operated, so that it can compute flows, pressures and water quality (e.g. disinfection concentrations and water age) throughout the network for a specific period of time.
It is capable of simulating complex WDN infrastructure and obtain all main hydraulic values by a demand-driven analysis (DDA) and a pressure driven analysis (PDA). 

For each scenario we consider two files, the node file focused on the WDN node structure and the link file focused on network pipe that connect junction or node.
To create the present dataset, we decide to output these values in a "DotComma-separated values" (\textit{CSV}) file with the following fields to take account the node:

* hour: A timestamp representing the time-interval we are currently watching in the simulation
* nodeID: Unique ID of a node inside the network
* demand: Rate of water withdrawal from the network. A negative value is used to indicate an external source of flow into the junction
* head: Hydraulic head (i.e., elevation + pressure head) of water in the node of the WDN
* pressure: Measured pressure in the node of the WDN 
* x_pos,y_pos: Coordinates of the node 
* node_type: A string which tells the type of the node (i.e., ”Junction”, ”Reservoir”, ”Tank”)
* has_leak: A boolean (True/False) which tells if a leak is present on that specific node (i.e., if we have a hole leaking water)
* leak_area: Area of the hole (m2)
* leak_discharge: Leak discharge coefficient. Takes on values between 0 and 1 
* current_leak_demand: The current simulation leak demand at the node. The total demand of a node can be viewed as: demand + current_leak_demand

and a file with the following fields to take account the link 
* hour: A timestamp representing the time-interval we are currently watching in the simulation
* linkID: Unique ID of a link inside the network
* link_type: A string which tells the type of the node (setted with "link")
* start_node: The source node of the link
* end_node: The target node of the link
* flowrate: The flow rate of the water inside the pipe at the current timestamp
* velocity: The velocity of the water inside the pipe at the current timestamp


