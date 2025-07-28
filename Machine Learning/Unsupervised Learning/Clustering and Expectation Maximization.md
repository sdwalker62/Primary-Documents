
Given a set of objects $X$ and inter-object distances $D(x,y)=D(y,x)$ for $x, y \in X$ we want to partition $X$ such that $P_D(x) = P_D(y)$ if $x$ and $y$ are in the same cluster.

# Single Linkage Clustering

- Consider each object a cluster ($n$ objects)
- Define inter-cluster distance as the distance between the closest two points in the two clusters.
- Merge two closests clusters 