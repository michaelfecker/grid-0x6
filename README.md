# Procedural generation

Recently, I came across some awesome-looking videos describing the procedural generation of various grids. Some of these used rectangles, triangles, or hexagons as a starting point. One of the videos I found most interesting was one showing the iterations of how the grid evolved with each iteration. Starting with an evenly structured grid, it became more and more naturally looking. 

## Idea

In general, the following steps will be performed to generate such a grid:

1. Create a hexagonally aligned set of vertices. These vertices are created in layers. Layer 0 represents the middle point of the hexagon, while each further layer is another, bigger hexagon.      
   ![Set of hexagonally aligned vertices in a set of layers](/example/010_vertices.png "Set of hexagonally aligned vertices in a set of layers")  
2. Build triangles with the previously created vertices.   
   ![Triangles connecting the previously created vertices](/example/010_triangles.png "Triangles connecting the previously created vertices")  
3. Add new layers with more triangles (optional). 
4. Compute the neighboring triangles for each triangle.
5. Randomly (or at least pseudo-randomly) combine two adjacent triangles into a parallelogram. Each triangle may only be part of one parallelogram.   
   ![Parallelograms merging two triangles](/example/010_parallelogram.png "Parallelograms merging two triangles") 
6. Some of the triangles may not find an adjacent triangle which is not merged into a parallelogram. This creates an irregular structure.   
    ![Unmerged triangles highlighted in orange color](/example/010_unmerged.png "Unmerged triangles highlighted in orange color") 
7. Each paralellogram is split into four quadrangles. These quadrangles are also parallelograms on their own.  
    ![Split parallelograms into 4 same-sized shapes](/example/010_patch-1.png "Split parallelograms into 4 same-sized shapes") 
8. Each remaining triangle is split into three quadrangles.  
   ![Split unmerged triangles into 3 same-sized shapes](/example/010_patch-2.png "Split unmerged triangles into 3 same-sized shapes")
9. Now, the magic happens (or in other words: this is where the algorithm really starts). The aim is to have a grid with similarly sized shapes, whereas the previous steps created shapes of two sizes: The shapes created from split parallelograms are bigger than the ones created from the split triangles. (to be precise: a shape created from a split parallelogram is 1.5 times as big as a shape created from a split triangle. A triangle is split into three shapes, while a parallelogram - which is two triangles - is split into four shapes).
   The following iterations shall try to create similarly sized shapes. 
