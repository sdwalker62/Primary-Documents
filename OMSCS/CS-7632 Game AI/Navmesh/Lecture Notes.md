---
title: "Path Planning: Navigation Meshes Introduction"
author:
  - Dr. Jeff Wilson
tags:
  - cs7632
link: https://mediaspace.gatech.edu/media/2021+Game+AI+-+Navmesh+-+Intro/1_fxkopdxu
---

# Path Planning: Navigation Meshes Introduction
## Non - Uniform Representation of Navigable Area

- **Grid** **Lattice** is a uniform structure with implicit mapping to game world coordinates.
	- $(\text{grid}_x, \text{grid}_y), \text{gridWorldCorner},$ and $\text{cellWidth}$ maps to different cell boundaries in world coordinates. ==This means we do not need a lot of memory for storage and this if very efficient per cell.==
	- World coordinates derived on demand
- We can switch to non-uniform structure with explicit mapping to allow for dynamic discretization
- Note we need more memory per discretized unit if non-uniform. So, we want the flexibility to be beneficial overall!

## Navmesh

- Instead of a square, we could allow arbitrary shapes (polygons)
- But we probably don't want to allow any possible polygon!

![[Pasted image 20250614121140.png]]

## Convex Polygon

- Easier to work with computationally
	- Efficient point containment test
		- Iterate through points CCW testing `LeftOn(a, b, pt)`
	- Efficient segment/ray intersection test
		- Iterate through points CCW tests line segment intersections and point containment
- Nice features for representing navigable space
- From any point on/in a convex polygon can directly reach (or see) any other point on/in the polygon

![[Pasted image 20250614121540.png]]

Difference between Path Network and Navmesh for navigating Stormwind: 

![[Pasted image 20250614121727.png]]

## Navmesh Connectivity

- Defines navigable polygonal areas with convex regions
- Adjacent edges define graph connectivity

![[Pasted image 20250614122021.png]]

![[Pasted image 20250614122032.png]]

---

# Navmesh Building

Now we will look at generating a Navmesh.

## Generating a Navmesh

- Greedy algorithm
- Other triangulation algorithms
- Recast and NEOGEN
	- Voxel based approaches for multi-level (2.5 dimensions)
	- Unity similar (possible Recast licensed)
	- https://github.com/recastnavigation/recastnavigation
	- https://www.cs.upc.edu/~npelechano/NEOGEN.pdf

## Greedy Navmesh Generation

- Goal: Create triangles exhaustively through scene
- Iterate through all obstacle/boundary points selecting point $a$
- Then iterate through all obstacle/boundary points selecting point $b$
- Then iterate through all obstacle/boundary points selecting point $c$
- This defines a candidate triangle...

## Greedy Triangle

- If the candidate triangle (normalized to CCW (counter-clockwise)) is valid with a non-zero area and does not intersect with the obstacles and the current list of formed triangles, then add it to the tri-list
- Otherwise, consider the next possible triangle
- Continue until no more triangles can be created

## Greedy Performance Improvements

- Rather than test the entire triangle, consider each edge
- A candidate tri-edge that is also an obstacle edge is valid
- However, a candidate tri-edge that intersects with an obstacle is not
- ==As soon as an edge fails, abandon it and try the next point pair==
- The iteration process itself (nested loops 3 deep) can be improved such that vertexes are not repeated
- $n \choose k$ where $k=3$
- Example:

```C#
for (i = 0; i < len - 2; ++i)
	{
	for (j = i + 1; j < len - 1; ++j) 
	{
		for (k = j + 1; k < len; ++k)
		{
			// i, j, k are indices into candidate point array/list
		}
	}
}
```


> [!WARN] Already Complete
> In the homework this is already done for you!

- Even with optimized indexing, there will still be repeated edges
- The intersection tests (and similar) for an edge can be stored in a hashtable-based data structure so that is they are revisited the cached value can be used

## Greedy Problem - Navmesh Adjacency Blocking

- Can form triangles that block adjacency 
- Greedy formation of `tri(ADF)` blocks adjacency of `tri(BEC)`
- **Red line** denotes a blacked adjacency
- `tri(ABF)` is a better place to start!

![[Pasted image 20250614133720.png]]

## Fix Greedy Problem

- Add an additional screening test for edges
- Check if a candidate tri-edge has any obstacle vertices *between* (collinear and intersecting) the edge endpoints
	- skip the edge if so
- This resolves the Navmesh adjacency blocking problem!

## Greedy Problem - Degenerate Triangles with Floating Point

- The *between* test can become fragile with floating point due to inconsistency with Epsilon values
- Use of *between* and degenerate triangle test of candidate triangle must agree!
- Inconsistency might occur part way through a fan of triangles
- This also blocks adjacency
- ==Use integers!==

![[Pasted image 20250614134355.png]]


## Greedy Problem - Long, Skinny Triangles

- More likely to have bad effects during gameplay (with float representation)
- Results in poor path quality
- There are algorithms with better quality such as Delaunay triangulation

> [!WARN] Slow!
> This process is slow (on the order of $O(n^4)$)

## Greedy - Edge Obstacle Intersection

- Many intersection tests are worst case
- Often testing two vertexes of the same obstacle
- Only want interior intersection to count as intersecting
- Need special case test for this!
- Once candidate triangles are formed, also need to test for obstacles fully inside and also check if the obstacle perfectly matches triangle

![[Pasted image 20250614135708.png]]

## Other Triangulation Techniques

- Many triangulation techniques
- Any algorithm considered should handle complex polygons with holes
- Constrained Delaunay triangulation
- Generally want triangles that are *not* long and skinny
- Can be as good as $O(N \log N)$
- `poly2tri` - https://github.com/greenm01/poly2tri

## Recast (and similar implementations)

- Voxels allow for simplification of navigable surfaces and identification of multiple levels

![[Pasted image 20250614140744.png]]\

## Navmesh Adjacency

- Once all Navmesh polys have been created, common edges can found among them to identify adjacency
- Can use a hashtable of edges for quick matching
- Note that a common edge connecting two CCW polys will be ordered opposite of its neighbor (e.g., $AB$ and $BA$)
- Hash code can be based on dot product of $A$ and $B$ to be order invariant (commutative property)

## Triangle/Polygon Merging

- Triangles/Polygons can be greedily merged
- This can simplify search graph for better search performance
- Leverages efficient adjacency tracking hashtable
- Merge two polygons into candidate polygon then test if convex
- If so, replace the two merged triangles and update adjacency hash table
- Repeat until no more polygons can be merged

## Navmesh PathNodes/Waypoints

- Iterate through the merged polygons following adjacent edges to create the nodes and edges
- A position must be decided for the nodes (and number of nodes per polygon)
- This is to support `A*` heuristic estimates (such as Euclidean Distance)
- And the actual path for agent to follow

---

