#Dataset output

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

