# Procedural generation of a rectangular grid with within a hexagonal shape.

Recently, I came across some awesome-looking videos describing the procedural generation of various grids. Some of these used rectangles, triangles, or hexagons as a starting point. One of the videos I found most interesting was one showing the iterations of how the grid evolved with each iteration. Starting with an evenly structured grid, it became more and more naturally looking. 

In general, the following steps have to be performed to generate such a grid:

1. Create a hexagonally aligned set of vertices,  
   ![Set of hexagonally aligned vertices in a set of layers](/example/010_vertices.png "Set of hexagonally aligned vertices in a set of layers")  
3. Build triangles with the previously created vertices,  
   ![Triangles connecting the previously created vertices](/example/010_triangles.png "Triangles connecting the previously created vertices")  
5. Add new layers with more triangles (optional)
6. Compute the neighboring triangles for each triangle,
7. Randomly (or at least pseudo-randomly) combine two adjacent triangles into a parallelogram. Each triangle may only be part of one parallelogram.  
   ![Parallelograms merging two triangles](/example/010_parallelogram.png "Parallelograms merging two triangles") 
9. Some of the triangles may not find an adjacent triangle which is not in another parallelogram. This will create an irregular structure.  
    ![Unmerged triangles highlighted in yellow color](/example/010_unmerged.png "Unmerged triangles highlighted in yellow color") 
11. Each paralellogram is split into four rectangles.
12. Each remaining triangle is split into three rectangles.
