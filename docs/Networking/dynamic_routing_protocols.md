# Introduction to dynamic routing 
Configuring routes manually can be a working solution in very small topologies, but becomes impractical as soon as it grows in size or in complexity. Dynamic routing algorithms allow routers to communicate with each-other so as to automatically route traffic through the right nodes, and to react automatically in case of a topology change (i.e. node failure or node addition).

Dynamic routing protocols are categorized in two main categories: 
- **Interior Gateway Protocols (IGP)** are meant to be used inside an isolated company or autonomous system.
- **Exterior Gateway Protocols (EGP)** are meant to be used between autonomous systems. The most well-known protocol is BGP.

Within the interior gateway protocols, two types of dynamic routing protocols can be differentiated:
- **Distance vector routing protocols** do not map the entire topology. All a specific router knows about the network to reach is which "path" (i.e. next hop or interface) to take, and how far away it is. Common distance vector protocols include RIP (v1 and v2) and EIGRP.
- **Link state routing protocols** communicate with all the other routers to build a network topology map common to all routers. Common link state protocols include OSPF and IS-IS.

## OSPF (Open Shortest Path First)
OSPF is an IGP and link state routing protocol. It uses [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra's_algorithm) to calculate the shortest path between nodes ([see video](https://www.youtube.com/watch?v=pVfj6mxhdMw&t)).

Steps are as follows:
1. Routers send "Hello" packets with all necessary informations on all their OSPF-enabled interfaces to find compatible neighbours.

To be compatible, both connected routers must follow these requirements:
- Both routers have a unique Router Identification Digit (RID)
- Area ID is the same
- Subnet is the same
- "Hello" and "Dead" interval are the same
- Authentication is properly set up
- Stub area flag is the same

2. Once compatible neighours are found, if there are more than 2 routers in the same subnet, routers elect a DR (Designated Router) and a BDR (Backup Designated Router) based on their RID. Routers then share LSAs (Link State Advertisment), containing informations about the links they are connected to and their cost (the cost is based on the link speed). If a DR has been elected, it acts as a single point to receive and broadcast LSAs, to ease bandwidth usage.

3. After all LSAs have reached all the routers, routers have enough information about the other nodes and their links to build the LSDB (Link State Database) and use Dijkstra's algorithm. The final result is an SPF Tree specific to each router, containing the fastest route to all the topology's network.

