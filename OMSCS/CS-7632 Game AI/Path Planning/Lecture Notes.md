## Motivation

- With movement behaviors, our agent knows how to seek a goal.
- But what if there is something in the way? What do we do?

In some cases we might be able to slide around the object. This could be part of the agents frame-to-frame movement decisions.

![[Pasted image 20250531175655.png]]

There is always a cell you could move to that decreases the distance between your agent and the goal. This is basically a heuristic pathfinding where the heuristic is the current distance between the goal and the agent. The problem though is that the agent can get stuck in a local minima or maxima.

![[Pasted image 20250531175906.png]]

We need some way to keep track of path choices that the agent is making and explore possibilities until an acceptable solution is found. In order to facilitate this planning we need a data structure that allows us to represent different possibilities for moving around in the environment and understanding where obstacles are. For this purpose we will use a graph. A graph contains the following:

- *Nodes*: 2D position or cell in the environment
- *Edges*: Valid paths that exist between nodes. This may be a line-of-sight path for traversal. This can be weighted where the weight represents the cost of traversal in a measurement such as energy or time. The edges might also be bi-directional or unidirectional depending on how movement is designed in the game.

There a few different graphs we might encounter:

![[Pasted image 20250531180357.png]]

Many games can be represented by a graph. For instance we can represent the states of the board game *Risk* as a graph:

![[Pasted image 20250531180540.png]]

## Planning

- Part of intelligence is the ability to plan
- Move to a goal
	- A Goal state
- Represent the world as a set of *States*
	- Each configuration is a separate state
- Change state by applying *Operators*
	- An Operator changes configuration from one **state** to another **state**
- *States*
	- Location of Agent/NPC in space
	- *Discretized space*
		- Tiles in a tile-based game
		- Turn 3D surface to pixels (grid lattice)
		- Floor locations in 3D
		- Voxels (https://en.wikipedia.org/wiki/Voxel)
		- Waypoints/"breadcrumbs"
		- Navmesh (https://en.wikipedia.org/wiki/Navigation_mesh)
- *Operators*
	- Move from one discrete location to next
	- Modifies state of modeled world, hopefully moving towards goal state
- **Graphs facilitate formal planning**

## Basic Strategy for Path Planning in Games

- Create a data structure (a graph) that facilitates path planning
	- Discretize the game world if necessary
- *Quantize* the Agent and Goal locations to the graph
- Perform path creation with a search algorithm
- *Localize* the path back to the game world
- Optionally clean up the path to look more natural
- Agent moves to follow path until goal reached

## Path Planning Algorithms

- Must **Search** the state space to move agent to goal state
- Computational issues:
	- *Completeness
		- Will it find an answer if one exists?
	- *Time complexity*
		- How long will it take?
	- *Space complexity*
		- How much memory will it take?
	- *Optimality*
		- Will it find the best solution?

## Search Strategies

- *Blind search*
	- No domain knowledge
	- Only goal state is known
- *Heuristic search*
	- Domain knowledge represented by *heuristic rules*
	- Heuristics drive low-level decisions
	- Video games provide domain knowledge that can be leveraged

The first blind search we will examine is *Depth First Search*:
* Always expand the node that is deepest in the tree
* Not best solution (if you stop at first found)

![[Pasted image 20250601120800.png]]

Depth first search has many flaws:
- It is not always optimal
- It often back tracks and heads in the wrong direction right from the start
- DFS is not really the best algorithm to use for path planning

*Breadth-First Search*
- Expand Root node
	- Expand all Root node's children
		- Expand all Root node's grandchildren
- This can return a good result if edges are all same weight or unweighted
	- If the edge weights vary it may not always yield an optimal path
- The problem is that the memory size can be too large

![[Pasted image 20250601121133.png]]

## Issues

- Failures when graph representation or intended path is not coordinated with:
	- The AI Agent Entity (vehicle)
	- Simulated space (the environment)

## Tile-based Games

- (Usually) 1-to-1 coordination of path-planning graph and simulated space
- AI exist in discrete locations
	- Can animate interpolated between cells, but they cannot stop in-between cells and must fully transition from one cell to another (tile)

## Grid Navigation

- 2D tile representation
	- Squares (4- or 8-way connectivity)
	- Hex (6-way connectivity)
- Often enforce one unit/entity per cell
- Each cell has terrain type
- Traversable or not

## Discretization of Continuous Space

- How to generate?
- Validity
- Quantization
- Localization
- Agent Movement
- Search Efficiency

## Generation

- Determine boundaries and terrain type regions
- ...but often a gradient
	- uphill
	- downhill
	- Shallow to deep water
	- etc.
- Verify world boundaries don't go through grid lines
- Verify no obstacle point within a grid cell, or vice versa
- Verify obstacle edge does not intersect grid cell edge
- Sometimes useful to mark both edges and cells as traversable (can help NPC get back on navigable grid if on a partially blocked cell)

## Grid Cells Point Containment

- Could treat as a polygon
- However, we have some standardized structure we can take advantage of
- Axis-aligned dimensions
- Can perform range checks for $x$ and $y$ dimensions
- Use less-than/greater-than for inside
- Use less-than-equal/greater-than-equal for on or inside
- Alternatively, with integer representation shrink cell dimensions by 1 unit for inside test with less-than-equal/greater-than-equal

## Problematic Edge Case

- Don't want the orange cells marked untraversable
- Could test only for proper line segment intersections
- But...

![[Pasted image 20250601124319.png]]

- ...then we would fail this case
	- ![[Pasted image 20250601124726.png]]
	- Cell would not be marked untraversable
- Easy fix: shrink the cell integer dimensions by 1 unit and use those edges for intersection testing (full proper + improper) with polygon edges
- Poly point containment test then catches this case

## Validity

- *Validity*: Consider A,B are nodes in a discretized space. From any point in node A, can an agent travel in a straight line to any point in adjacent node B?
- (For grid lattice, generally only applicable with continuous space)

![[Pasted image 20250601124902.png]]

## Off Grid? 

- What to do if an AI entity is off a navigable grid cell?
	- Local character movement with ray casting and straight-line movement
- Cells marked as not traversable can still have meta data denoting edges that are fully/partially passable (validity)
- Random movement and physics engine to slide/bump around and hope to eventually get to a valid position
- Just cheat and teleport (especially if the game player isn't looking)

## Continuous Position/Movement versus Path from Discrete Graph

- Awkward/blocky movement
- Post process path
	- *"string pulling"*
- Steering behavior at runtime (greedy)
	- May need to augment the environment (special colliders for pits, etc.)

![[Pasted image 20250601125522.png]]

## Post Process (String Pull)

![[Pasted image 20250601130028.png]]

## Search Efficiency with a Grid Lattice

- Search algorithm must visit a lot of nodes
- Search space grows quickly
- $N \times N$ grid $\rightarrow$ $N^2$ nodes
- $((N-1) \times N) \times 2_{\text{xy\_dims}} \times 2_{\text{bidirectional}}) \rightarrow$ 4-Way Edge Count
- $(N-1) \times (N-1)) \times 2_{\text{angle\_dims}} \times 2_{\text{bidirectional}}) \rightarrow$ extra 8-Way Edge Count
- But nodes and edges can be generated on the fly
- Poor choice for sparse environments!

## Summary 

- **Pros**
	- Easy to implement
	- Work well for games that are inherently tile based (discrete movement)
	- Supports temporary obstacles easily (e.g. other units)
		- Good for multiple unit movement (group movement)
	- Implicit node/edge representations with on demand querying
- **Cons**
	- Not great for continuous environments 
	- Can be a burden on search efficiency
	- Poor path quality
