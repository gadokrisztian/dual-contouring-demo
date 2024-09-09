# dual-contouring-demo
My implementation of the Dual-Contouring algorithm.
![loading gif](media/dc_demo.gif)

It samples the following implicit distance function:
```python
rect_outer = Rectangle(0.0, 0.0, 0.5, 0.5)
rect_inner = Rectangle.from_corner(-0.5, -0.3, 0.3, 0.2)
c1 = Circle(-0.2, -0.2, 0.1)
c2 = Circle(0.2, 0.3*np.sin(np.deg2rad(theta*4)), 0.152)
sdf = Difference(rect_outer, rect_inner, c1, c2)
sdf = Rotate(sdf, theta)
```

 Starting with the samples, I construct the quadtree and 
 calculate the vertices of the cells that contain the 
 contour. To determine the vertex positions, I use a 
 standard quadratic error function along with mass-points. 
 Then, following the method from the original paper, 
 I generate contour lines connecting these vertices. Once 
 that's done, I balance the quadtree, ensuring neighboring 
 cells have a depth difference of no more than 1. The 
 meshing process happens in two steps: first, I mesh the 
 cells without contour lines, and then handle the rest. 
 After building the initial mesh, I apply Lloyd's 
 relaxation to the vertices to enhance the overall mesh 
 quality.
