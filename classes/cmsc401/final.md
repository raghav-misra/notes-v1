# cmsc401 / final

## primitives

**Polyline** is a chain of line segments.

- Simple if the segments are only connected at vertices, no overlaps.

**Polygon** is a **closed polyline**.

- Divides plane into *interior* and *exterior* regions.

**Region** is a subset of the plane which is:

- *Closed:* contains its boundary.
- *Bounded:* exists a circle in the plane containing the region.
- *Connected:* any pair of points can be connected with a line.
- *Regular:* does not have dangling parts.

**Simply connected region** when its complement is connected.

**Multiply connected region** when its complement is not connected.

**Polygonal region** is one whose boundary is defined by a polygon.

- **Multiply connected polygonal region** represented as a polygon which contains all the other polygons. None of the other polygons contain a polygon.
- Usually, polygon is oriented in counterclockwise. Internal boundaries of a multiply connected polygonal region are oriented in clockwise.

## point in polygon

**Point in polygon** is a very self-explanatory and important routine.

- Given polygon $PL$ and point $P$, decide one of the following.
  - $P$ is on the interior of $PL$. 
  - $P$ is on the exterior of $PL$.
  - $P$ is on $PL$. (Boundary)

General solution:

- Consider half-line starting at $P$ going outward. Let $k$ be the number of intersections between a boundary of $PL$ and the half-line.
  - Hitting a vertex counts as two intersections. 
  - If the half-line runs along an edge, ignore it. *Except when $P$ lies on the edge.*
- If $k$ is odd, $P$ is on the interior of $PL$.
- If $k$ is even, $P$ is on the exterior of $PL$.
- If one of the intersections is point $P$ itself, $P$ is on $PL$. (Boundary)

## convex hull

**Convex hull** of a point set is smallest wrapping containing all the points.

- Elastic band intuition.

Two problems:

1. Computing the convex hull itself.
2. Identifying the extreme vertices (of the convex hull).

*Simple solution to problem 2:*

- For every point, check if it is on the interior or the boundary of any triangle formed by every three points.
- If so, it is not an extreme point. Else, we keep it as an extreme vertex.

**Graham's Algorithm.**

- Pick a point $O$ and sort the points in $S$ based on angle from $O$.
- Start at rightmost and go counterclockwise. If left turn is made, likely to be in the hull. Else, not in the hull.

## vector/raster data models

**Discrete object view** is a collection of discrete countable objects which can be assigned to different classes. Like trees and houses and roads.

**Continuous object view** is a collection of continuous surfaces representing variation of properties, like temperature or elevation.

**Vector data model** (discrete object view) has objects represented as points and lines and polygonal regions.

- Regions are combined to form maps.
- Lines are combined into networks. (Roads, rivers, etc.)
- *Data representation.*
  - Point is its $(x, y)$.
  - Line is *simple polyline*, sequence of points.
  - Region is encoded with its bounding (simple) polygons.
- *Pros and cons.*
  - High accuracy and resolution.
  - Compact data representation.
  - Connections are described explicitly.
  - Easy updating.
  - But: more complex and set operations are computationally intensive.

**Raster data model** (discrete object view) has everything represented as pixels on a grid.

- Point is a single pixel.
- Line and regions are collections of connected pixels.
- Data is not encoded beyond the pixels themselves.
- *Data representation.* Everything is pixels! Encoded in square matrix $M$.
  - The number of cells in $M$ determines resolution.
- *Pros and cons.*
  - Simple.
  - Geospatial data is often directly read as raster data.
  - Set operations are easier based on pixel pairing.
  - But: large size for high-res and low-res means missing data. Difficult to detect object boundaries.

**4-connectivity** and **8-connectivity**.

- If two pixels are connected by an edge, **4-adjacent**.
- If two pixels are connected by a corner, **8-adjacent**.
- If you can hop across **4-adjacent** pixels to get from $A$ to $B$, then $A$ and $B$ are **4-connected**. 
- Similar idea for **8-connected**.

## point data grids

**Point** is $(x, y)$ tuple.

**Query** is a request for data points in $S$ which satisfy a condition.

- Need a data structure with support for efficiently executing common queries.

Basic operations on point data.

- *Update.* Insert or delete a point in $S$.
- *Point query.* Is a point in $S$?
- *Range query.* Find $S' \subseteq S$ which contains all points in a bounding box.
- *Nearest neighbor query.* Given a point $Q$, find the point in $S$ closest to $Q$.
- *$k$-nearest neighbor query.* Same idea extended to many points. Return in order such that closest points appear first.

A **grid** subdivides domain $D$ into cells. Each cell contains a subset of the points in $S$.

- *Point query.* Find corresponding cell and examine its points.
- *Point insertion.* Find corresponding cell and add new point, if not already there.
- *Point deletion.* Find corresponding cell and delete point, if it exists.
- *Range query.* Cells strictly in the box will contribute all their points. Cells which intersect partially with the box will need to be examined to only take the overlapped points.
- *Pros and cons.* Grid is simple and has constant cell access. However, only good for uniformly distributed points due to fixed resolution across the grid. Dynamic resolution is achievable with trees.

## point region quadtree

**PR-quadtree** represents a set of points $S$ across a domain $D$ where the points of $S$ are distributed.

- It subdivides $D$ into nested square regions. $4$ at each level.
- Every block of the decomposition is either empty or contains one point.

When a block contains more than one point, it must be split.

- Block is subdivided into NW, NE, SW, SE quadrants. Four children.
- This subdivision is done recursively until each block either contains exactly one point in $S$ or is empty.

Algorithms on point data.

- *Point query.* Recursively descend through the tree until the block with this point is reached. If exists, return it; else, do nothing.
- *Point insertion.* Locate the leaf block which contains or would contain $P$. 
  - If $P$ exists, do nothing. 
  - If the block is empty, add $P$.  
  - If the block is full, subdivide it further into more blocks until $P$ and the existing point can coexist in their own leaf blocks.
- *Point deletion.* Locate the leaf block which contains or would contain $P$. 
  - If $P$ doesn't exist, no need to do anything.
  - If $P$ exists, transform the block into an empty leaf.
    - Merge back outwards to collapse levels of empty subtree.

## terrain data modeling

Recall *discrete and continuous object views*.

A **scalar field** maps every location to a value.

- In our case, something like temperature or elevation.
- $z = f(x, y)$ takes in the point and returns the scalar.

**Digital elevation model.**

- Set of points $V$ at which the elevation is known.
- Partition of domain $D$ into cells with vertices at points of $V$.
- Interpolation function to approximate elevation everywhere else.

**RSG-Regular square grids** is where the domain partition is a uniform grid.

- Regularly distributed data points. Vertices at the points of $V$.
  - Elevation values are also there.
  - You use an interpolation function. 
- Encoded with a 2d grid of cells, each point containing list of vertices in that cell.

**TIN-Triangulated irregular networks** is where the domain partition is a triangle mesh.

- Explained in later lecture.

## point-region kD tree

Same thing as a quadtree but instead of splitting into quadrants at every level, you split into halves at every level.

Depending on the level, you alternative between splitting into horizontal and vertical halves.

## point and mx quadtrees

**Point quadtrees.** Split *at the points* rather than rigid quadrants or halves.

- Intermediate nodes can also contain vertices, as they are used as the split points.
- *Point query.* Basically same as all else. Traverse and see if you find it.
- *Insertion.* Look for the right leaf, unless you find it in an intermediate node. If no leaf, find the point in the lowest leaf and split along it.

**MX quadtrees.** Hierarchical representations for sets of points.

- Similar to region quadtrees.
- Points are *black pixels* and empty blocks are white pixels.

## triangular irregular networks

**Triangle mesh** is a triple $M = (V, E, T)$.

-  $V$ is a finite set of points in the plane.
- $E$ is a set of edges connecting points in $V$.
- $T$ is a set of triangles connecting the vertices of $V$.
- Two triangles either intersect (common vertex or edge) or they don't.

Meshes are the domain partitions for **TINs**.

The data structures for meshes encode the vertices, edges, and triangles, but also the **connectivity relations** between single entities.

- *Triangle vertex* associates a triangle with its bounding vertices.
- *Triangle edge* associates a triangle with its bounding edges.
- *Triangle triangle* associates a triangle with the triangles around it that share an edge.
  - Two triangles with this relation are **adjacent**.
- *Vertex edge* associates a vertex with its incident edges.
- *Vertex triangle* associates a vertex with its incident triangles.
- *Vertex vertex* associates a vertex with all the vertices its connected to via a single edge.
- *Edge vertex* associates an edge with the two vertices it connects.
- *Edge triangle* associates an edge with the two triangles who have it as a side.
- *Edge edge* associates an edge with all the other edges connected to its vertices.

**Indexed data structure** is the simplest data structure for triangle meshes.

- It encodes $V$ (vertices) and $T$ (triangles).
- Edges are not stored explicitly.
- *Relation encoded:* Triangle vertex.
- *Implementation.*
  - Vertex table stores coordinates and attributes associated with each vertex.
    - Such as elevation in the case of a TIN.
  - Triangle table stores indices of each triangle and possibly other attribute.
- *Queries.*
  - Triangle vertex is a constant time lookup. Look at triangle table.
  - Any relation other than triangle vertex is linear because you need to search everything.

**Indexed data structure with adjacencies.**

- It encodes $V$ (vertices) and $T$ (triangles).
- Edges are not stored explicitly.
- *Relation encoded:* 
  - Triangle vertex (as with indexed)
  - Triangle triangle
  - PARTIAL Vertex triangle. (For each vertex, just one triangle.)
- *Implementation.*
  - Vertex table stores coordinates and attributes associated with each vertex.
    - Index in the triangle table of one triangle incident. (Partial VT)
    - Elevation in the case of a TIN.
  - Triangle table stores vertex indices AND indices of the adjacent triangles.

**Refining triangle mesh.**

- *Triangle split.* Add new vertex into a triangle. Split the existing triangle into three, based on the new vertex.
- *Edge split.* Insert a new vertex $v$ onto an edge and split it and the two incident triangles into two.

## voronoi and delaunay

Given a point $p$, it has **Voronoi region** $R_v(p)$.

- A given point $q$ not in $V$ is part of the locus $R_v(p)$ if $p$ is its nearest neighbor.

Remarks:

- Voronoi regions are not necessarily bounded.
- May contain several unbounded regions. 

**Neighbor-finding query.** Build Voronoi diagram. See which region the query point is in. Return the vertex of that region.

A **triangulation** of a set of points $V$ is a triangle mesh $M = (V, E, T)$ such that the mesh vertices correspond with the set of points. Also, the convex hull of $V$ is the domain of $M$.

A **Delaunay triangulation** has more specific requirements.

- No point lies inside the circumcircle of any triangle in the triangulation.

**Delaunay triangulation is the dual of Voronoi region.**

- Delaunay is formed by connecting all pairs of points whose Voronoi regions share an edge in common.
- It is bounded by the convex hull of the set of points.

**Watson's algorithm.** 

- Incremental algorithm for building a Delaunay triangulation.
- Add one point by one point at a time.
- Convex hull. Convert into basic triangulation.
- Add point and delete the mismatching triangles by detecting its region of influence.
- Repeat for all points.
- Steps:
  - Detect influence region.
  - Delete the triangles in the influence region.
  - Retriangulate by joining $p$ to the vertices of the influence polygon.

## map representation

**Immersion of graph** draws edges as curves.

**Planar graph** is one with an immersion such that no edges intersect.

A **map** is a planar graph of vertices, edges, and faces.

- The graph $(V, E)$ is connected.
- See how a triangle mesh is an example of a map!

In a **polygonal map**, the edges are straight line segments.

**Slab method.**

- Looking for a point $p$ on the map.
- Partition map into vertical slices. (Draw line through each vertex.)
- Store sorted list of slab $x$-coordinates and use binary search (bisection) to find the right slab which would contain point $p$.
- And then you find the region/edge/vertex in that slab which contains the point.

## terrain segmentation

**Critical points** are minima, maxima, saddle.

- Saddle point increases in one direction and decreases in the other.

You can use first and second derivatives to first determine which points are critical and then how to classify them.

For a TIN,

- **Maximum:** $f(v) > f(x)$ for adjacent vertices $x$.
- **Minimum:** $f(v) < f(x)$ for adjacent vertices $x$.
- **Saddle:** The *link* of $v$ has at least two subsequences with values specifically lower or greater than $f(v)$.

**Critical net.** Points and separatrix lines.