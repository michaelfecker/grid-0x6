# Procedural generation of a rectangular grid with within a hexagonal shape.

Recently, I came across some awesome-looking videos describing the procedural generation of various grids. Some of these used rectangles, triangles, or hexagons as a starting point. One of the videos I found most interesting was one showing the iterations of how the grid evolved with each iteration. Starting with an evenly structured grid, it became more and more naturally looking. 

In general, the following steps have to be performed to generate such a grid:

1. Create a hexagonally aligned set of vertices, ![alt text](./example/010_vertices.jpeg)
2. Build triangles with the previously created vertices,
3. Add new layers with more triangles.
4. Compute the neighboring triangles for each triangle,
5. Randomly (or at least pseudo-randomly) combine two adjacent triangles into a parallelogram. Each triangle may only be part of one parallelogram.
6. Some of the triangles may not find an adjacent triangle which is not in another parallelogram. This will create an irregular structure.
7. Each paralellogram is split into four rectangles.
8. Each remaining triangle is split into three rectangles.
