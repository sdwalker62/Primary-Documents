

## Alternative to Grid Lattices and Similar

- Abandon relying on structured area that implicitly defines a graph
- Instead, imagine overlaying a graph onto the game world

![[Pasted image 20250601131108.png]]

==We can have arbitrary edge lengths in the path network!==

## Path Network

- Graph nodes are associated with vector positions (points in game world)
- Graph edges are traversable line segments in the game world
	- The agent can follow the edge without being blocked

## Why Path Networks?

- Goal of reducing the memory (and path search burden) of dense grid lattices
- Can be sparse or dense as appropriate for variable game world details
- Can reduce the jagged nature of paths found on grid lattice

## New Agent Movement Paradigm

- With a path network, there is no navigable area defined for the area
- Only connected line segments
- This is a very small part of the game world!
- Thus, the agent is allowed two states for movement:
	- *Local movement*
	- *Remote movement*

## Path Network Movement

- When the agent is performing *local movement*, decisions are based on entities in sight of the agent (e.g. ray cast)
	-  Based on kinematic movement, steering behaviors, etc.
- When the agent needs to access something out of sight, the agent queries for a path and enters the *remote movement* state

## Remote Movement

- Agent can be **on** the path following from node to node and staying on or very close to the edges
- Agent may go **off** the path due to a dynamic obstacle, opportunistic task, emergency, etc.
	- The position upon leaving is saved ($leftPos$)
- Once off the path, the agent relies on local movement to get back on at $leftPos$
- If not possible, new path planning can be performed

## Design Implication

- To use a path network, local movement must be robust
	- Effective detection of obstacles, reliable movement on terrain of various types, etc.

## Path Network Example

![[Pasted image 20250601132246.png]]

The first step is to perform remote movement and we want to find the closest visible node:

![[Pasted image 20250601132330.png]]

This is a situation where the agent is going to query all of the local nodes and in the worst case (a naive implementation) we could check against every node in the graph. This would not be good for large game worlds. 

Once you have your neighborhood is determined, you can ray cast to all of the local nodes and see if there is an occlusion. In this scenario the agent is occluded from node A but not G. If the agent can see more than one node we move toward the one that is **closest**. 

![[Pasted image 20250601132559.png]]

We want to find the closest node to the goal. The goal can see two nodes M and N so we select the one that is closer which in this case is $N$ and set node $N$ as the goal.

![[Pasted image 20250601132705.png]]

We can perform some sort of search (say $A^*$) to find the fastest path and then perform remote movement along the returned path. 

At the end the agent moves along the tail to the pot of gold ($N \rightarrow \text{Goal}$). 

Some issues is that that the path quality is poor. Notice that the path has a double back at the end (why go to $N$ when you can go right to the goal?). 

![[Pasted image 20250601133130.png]]

Another problem is that the agent can get stuck if there are no nodes visible from the agent's location. This can happen when the agent spawns in a bad area or gets knocked into a bad area. 

![[Pasted image 20250601132959.png]]

One way to solve this is with dynamic nodes or if the player cannot see that agent we could teleport him to the nearest node to continue moving properly.

## How to Build a Path Network?

- *Manual Placement* 
	- Tedious, but can give good results
	- Can use manual node placement, but automatic edge forming
- *Automatic Placement*
	- Quick, but can be inefficient and temperamental
	- Might work on some levels but not others
## Path Network - Automatic Placement - Flood Fill

- Start with *seed*
- Expand by adding uniformly
- Designed might move, delete, add manually afterwards
- Ensure **all nodes and edges are at least as far from walls as agent's collider radius**
- Can be as dense as a grid lattice but loses out on the uniform structure memory savings!

![[Pasted image 20250601133558.png]]

## Points of Visibility

- Convex angle obstacle features create natural *inflection points* for efficient paths through the environment
- Optimal paths will always have inflection points at convex vertices
- These points are good candidates for path nodes!

![[Pasted image 20250601133913.png]]

- Real world maps need to be simplified (possibly use colliders) as too many points to be practical 
- Inflection points must be offset by some distance to leave room for agent
	- Offset along bisecting line of angle
	- Should be further than the radius of the agent to allow flexibility/buffer

### 1. Start with geometry and compute offset vertices by Agent radius

![[Pasted image 20250601134407.png]]

### 2. Determine visibility between nodes and edges

![[Pasted image 20250601134439.png]]

This tends to find natural efficient paths (e.g. agent hugs corners around obstacles)

### Points of Visibility Bloat

- Nodes and edges can explode combinatorically
- Can end up going down a rabbit hold of adding more and more auto-placement features that never quite work
- Often requires a lot of manual tweaks, offsetting the benefits

![[Pasted image 20250601134709.png]]

### Closing Remarks

- Concave angles *could* be used as well for better coverage of a navigable space (especially a boundary)
- Similar to previous convex angle offsetting, but you additionally need to find point on the angle bisecting line that is at least the agent's radius away from a line that is coincident with one of the two line segments of the convex angle.
	- Add some extra offset as well so agent doesn't get stuck (use slightly bigger radius)
- Concave angles are not path inflection points, so not very useful
- Probably better off adding extra nodes at points of interest

![[Pasted image 20250601135514.png]]

## Build a Path Network from Candidate Nodes

- Must evaluate whether an obstacle intrudes on corridor defined by edge between node $A$ and $B$ 
- Corridor size defined by agent radius
- This ensures that agent can traverse path $AB$ 
- Use combination of *point-distance-to-line-segment* test and *line-seg-line-seg-intersection* test
- If the corridor is clear, then add the edge to the graph

![[Pasted image 20250601135909.png]]

- Check if the edge between nodes intersects any of the edges of our obstacle
- A parallel check is to make sure that our nodes (or edge segments) are not too close to any obstacle or the boundary 
- The first failure that we encounter we should exit
- Order the test by which are more likely to fail so we can short circuit

## Quake Reaper Bot

- Created by Steve Polge
- Resulted in hire by Epic Games
- Built Unreal Tournament Bots
- Used handmade path networks
- Also, had *dynamic path network* mode

## Breadcrumbs/Dynamic Path Network

- Build dynamically (Hansel and Gretel)
- Agent "drop" waypoint at important locations
- Start with a waypoint at HOME location as first node of a graph
- Each $Think()$ update, check to see if from the current position can ray cast cleanly to the $lastWaypoint$ 
	- If yes, then store as $lastSafePos$ var.
	- If no, add $lastSafePos$ to graph as a new node and connect to $lastWaypoint$
		- Set $lastWaypoint$ to $lastSafePos$
- Additional incremental update process to form other edges
	- Space partitioning such as *cell-space/bin-space* to track nearby waypoints
- **Applications**
	- Could be useful in procedurally generated worlds that are impractical to pre-author or bake path planning into
	- Potentially avoid authorial burden of creating network
- **Disadvantages**
	- Runaway waypoint formation easts up memory
	- Clean-up process can become expensive

## Addressing Path Quality with Path Network

- *String Pulling* could be utilized but would need to work against world geometry (maybe physics colliders)
- Or agent could use *Greedy Path Following* approach 
	- Take advantage of the fact that the agent can be on or off the path

## Path Network: Greedy Steering

- Improve path by agent steering/skipping-ahead to furthest node in path that it can see
	- Use ray cast, but watch out for *pits*!
- May clip a corner
	- Use *point-dist-to-line-seg* to test
- Can also lookahead on edges through iterative subdividing
	- But more expensive

![[Pasted image 20250601141643.png]]
![[Pasted image 20250601141736.png]]
![[Pasted image 20250601141811.png]]

## Path Network: Greedy Steering - Problems

- Agent steering behavior ultimately is not a perfect solution to *fixing* path network quality problems 
- Ray casting will still miss some things
- Ray casting can easily become expensive!
- Especially problematic on variable height terrain and different terrain types
- Agent may take a shortcut but end up walking in slow terrain instead of staying on the path of fast terrain (e.g. mud versus road)

## Pros

- Discretization of space can be very small
- Doses not require agent to be at one of the path nodes all the time (unlike grid)
- Switch between local and remote navigation
- Works well with continuous movement agents
- Good for FPS, RPGs
- Nodes can include useful metadata (e.g. cover locations, etc.)

## Cons

- Valid agent positions might not be able to see a node in the network (cannot switch to remote movement)
- Jagged path shape
- Dynamic and rolling terrain issues
- Storage/complexity of network to get good coverage and good path shape (esp. auto gen)
- Agent going off the network path can be dangerous (getting stuck, etc.)
- Potentially puts a lot of real0time computational pressure on the agent implementation rather than on pre-processed discretization 

## Variable Size Path Network Corridors

- Each node has its own radius defining a clear zone around it
- AND connected nodes form a region (roughly a cone) along the connecting edge that is also clear
- Can allow for safe and efficient local movement (in convex regions)
	- Agent can avoid dynamic obstacles by moving within region
	- Opportunistic actions like loot collecting
	- Efficient string pulling (within the corridors)
- Concise corridor definition (2 $Vect2s$ & 2 floats)
- Modified *point-dist-to-line-seg* to efficiently test point containment
	- leverage line vector equation $t$ scalar to linearly interpolate between radiuses 
- Work with multiple agents of various radiuses, reduce each node radius by agent radius
- Downsides:
	- Challenging optimization problem to automatically maximize overall corridor area
	- Still doesn't fully represent navigable space
	- Cannot necessarily place node at obstacle inflection points (but may be within radius area)

![[Pasted image 20250601143105.png]]

