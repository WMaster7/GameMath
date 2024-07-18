<i><b>Required knowledge:</b>
- pythagoras theorem
- algebra (solving system of equations)
- getting distance between points
- 2d vectors
- rotating a 2d vector 90 degrees
- unit vectors / normalizing vectors
- dot product</i>

## Circle to Circle intersection Points

Lets find out how to find the intersection points of 2 circles with arbitrary positions and sizes. (or radiuses)<br>

![Circle Intersection Points 01](https://github.com/user-attachments/assets/90366021-1b09-4daa-b117-40be448395b7)

Lets first rule out some obvious cases. Let $d$ be the distance between both circle centers. Often, the circle center and its radius are known, so this will be assumed throughout.

&nbsp;&nbsp; $d = distance(c_1, c_2)$

(1) If the distance is larger than both radiuses combined, then they are out of range from one another, so there will be no intersection.<br>
(2) If the radius of one circle is larger than the distance plus the radius of the other circle, then the other circle is completely inside the first circle. Likewise, there will be no intersection.<br>

![Circle Intersection Points 03](https://github.com/user-attachments/assets/e17eaf05-62fe-4dd4-a886-2f2f7555bd6a)&nbsp;&nbsp;&nbsp;&nbsp;![Circle Intersection Points 02](https://github.com/user-attachments/assets/87fc7573-ca9d-43b2-afb8-27d138e0ed87)

You may choose to handle the situations where the circles touch from either the inside or outside. This happens when the combined radiuses are exactly the same as the distance, or when one radius is exactly the same as the other radius plus the distance.<br>

Continuing we will cover the case where there are 2 intersections.<br>

Notice that connecting circles from their midpoints will give symmetry on both sides. We can discard one side, work with semicircles and aligning to an axis for visual clarity.<br>

![Circle Intersection Points 04](https://github.com/user-attachments/assets/9fad4fd5-eb5d-470a-b349-cf96e9a53be4)&nbsp;&nbsp;&nbsp;&nbsp;![Circle Intersection Points 05](https://github.com/user-attachments/assets/2b09cf67-3d55-4a3b-b340-c17fb5551129)


