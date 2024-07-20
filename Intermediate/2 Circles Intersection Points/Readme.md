<i><b>Required knowledge:</b>
- pythagoras theorem
- algebra (solving system of equations)
- getting distance between points
- 2d vectors
- rotating a 2d vector 90 degrees
- unit vectors / normalizing vectors</i>

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

Notice that connecting circles from their midpoints will give symmetry on both sides, so we can ignore one side and work with semicircles. If we find one point, then we can reflect it along the axis to find the other too. Lets also align the axis to the horizontal axis for visual clarity.<br>

![Circle Intersection Points 04](https://github.com/user-attachments/assets/9fad4fd5-eb5d-470a-b349-cf96e9a53be4)&nbsp;&nbsp;&nbsp;&nbsp;![Circle Intersection Points 05](https://github.com/user-attachments/assets/2b09cf67-3d55-4a3b-b340-c17fb5551129)

If we draw a line from point $p$ down to the horizontal axis, we are able to construct two right-triangles and use the pythagoras theorem. Let $h$ be the distance from the horizontal at $p$ and let $x$ be the distance from $c_2$ to $p$ on the horizontal axis.

![Circle Intersection Points 06](https://github.com/user-attachments/assets/c49a31cb-591f-41ed-b659-6ee707d6aba2)&nbsp;&nbsp;&nbsp;&nbsp;![Circle Intersection Points 07](https://github.com/user-attachments/assets/ee3bcd94-1274-4cf5-a091-db5d5916a4df)


Distances $d$, $r_1$ and $r_2$ are known, while $x$ and $h$ are unknown. Since we have 2 unknowns, we create 2 equations for the 2 right-triangles.<br>

Triangle (1) with sides $h$, $r_1$ and $(d + x)$ gives:<br>

&nbsp;&nbsp; (1) $h^2 = r_1^2 - (d + x)^2$<br>

Triangle (2) with sides $h$, $r_2$ and $x$ gives:<br>

&nbsp;&nbsp; (2) $h^2 = r_2^2 - x^2$<br>

We can eliminate $h$, as we have 2 equations for $h^2$ and can thus aquate both right hand sides with eachother and solve for $x$.<br>

&nbsp;&nbsp; $r_1^2 - (d + x)^2 = r_2^2 - x^2$<br>

Expanding $(d + x)^2 = d^2 + 2dx + x^2$ and we have:<br>

&nbsp;&nbsp; $r_1^2 - d^2 - 2dx - x^2 = r_2^2 - x^2$<br>

Both sides include the $-x^2$ term, so these cancel.

&nbsp;&nbsp; $r_1^2 - d^2 - 2dx = r_2^2$<br>

We can isolate $-2dx$ and negate all terms by multiplying both sides with $-1$.<br>

&nbsp;&nbsp; $-2dx = r_2^2 - r_1^2 + d^2$<br>
&nbsp;&nbsp; $2dx = -r_2^2 + r_1^2 - d^2$<br>

To isolate $x$ we divide both sides by $2d$ and rearrange.<br>

&nbsp;&nbsp; $x = (-r_2^2 + r_1^2 - d^2) / 2d$<br>
&nbsp;&nbsp; $x = (r_1^2 - d^2 - r_2^2) / 2d$<br>

We can store $x$ and use it in one of the equations for $h^2$ to find $h$. Using equation (2) would be the simplest. Taking the square root of boths sides will solve for $h$.

&nbsp;&nbsp; (2) $h^2 = r_2^2 - x^2$<br>
&nbsp;&nbsp; (2) $h = \pm \sqrt{r_2^2 - x^2}$<br>

Note that $h$ now has 2 solutions, this is because of the square root operation. $h$ can be either positive or negative, which makes sense because we have symmetry along the horizontal axis for the two intersection points.<br>

Now that we know $x$ and $h$, we can now find the actual location of both intersections. Because we have value $d$, we can normalize the vector from $c_1$ to $c_2$ to get $n = (c_2-c_1)/d$. Rotating $n$ by 90 degrees in any direction of preference gives $n'$.<br>

To find the intersection, we take $c_1$ and add the normal vector $n$ multiplied by $d + x$ and add another $n'$ multiplied by either positive $h$ or negative $h$. This way, we move $d + x$ along the axis, and $h$ along the perpendicular, starting from $c_1$.<br>

![Circle Intersection Points 08](https://github.com/user-attachments/assets/b29a5e1a-e54e-4180-9d3f-c657a57d6df7)&nbsp;&nbsp;&nbsp;&nbsp;![Circle Intersection Points 09](https://github.com/user-attachments/assets/bec3ab01-938e-483b-9fe7-18f4a342b73a)

It's not required to have circle 1 or 2 ordered in any perticular way. They can be swapped, as long as their centers and radiuses remain correctly assigned in the equations.<br>

### Circles with equal Radiuses

Let's also have a look when 2 circles have the same radius. This states that $r_1 = r_2$ and we can simply call this radius $r$.<br>

Recall our equation for $x$ and replace $r_1$ and $r_2$ with $r$.<br>

&nbsp;&nbsp; $x = (r_1^2 - d^2 - r_2^2) / 2d$<br>
&nbsp;&nbsp; $x = (r^2 - d^2 - r^2) / 2d$<br>

We can see that we have a postive and a negative $r^2$ term, these cancel eachother and simplify our equation. We can then see that only $-d^2$ remains in the numerator, while we still divide by $2d$ This means that one multiplication or power of $d$ will also be canceled together with the division by $d$.<br>

&nbsp;&nbsp; $x = (-d^2) / 2d$<br>
&nbsp;&nbsp; $x = -d / 2$<br>
&nbsp;&nbsp; $x = -\frac{d}{2}$<br>

The result being that $x$ now is just the negative of half the distance between the circles. Since $x$ was an extension of $d$ to find the distance of the intersection along the axis, which now is negative, we can say that $(d + x) = (d - \frac{d}{2}) = \frac{d}{2}$. Meaning that the intersection always lies in the middle of 2 circles with the same radius. This makes sense when seeing a picture.<br>

![Circle Intersection Points 10](https://github.com/user-attachments/assets/34e08615-5fbb-45a8-a1f5-4a0d0d81e9ee)

Recalling our equation for $h$, which now is:<br>

&nbsp;&nbsp; $h = \pm \sqrt{r_2^2 - x^2}$<br>
&nbsp;&nbsp; $h = \pm \sqrt{r^2 - (-\frac{d}{2})^2}$<br>
&nbsp;&nbsp; $h = \pm \sqrt{r^2 - \frac{d^2}{4}}$<br>

## Summary

To summarize, we have the following equations when distance $d$ between the circle centers is calculated.<br>

![Circle Intersection Points 11](https://github.com/user-attachments/assets/923298c9-91fc-40b1-ab43-43c9e19b78c6)

&nbsp;&nbsp; $d = distance(c_1, c_2)$<br>
&nbsp;&nbsp; $x = (r_1^2 - d^2 - r_2^2) / 2d$<br>
&nbsp;&nbsp; $h = \pm \sqrt{r_2^2 - x^2}$<br>

We can then get normal vectors $n$ and its perpundicular $n'$. Rotating can be in any preferred direction.<br>

&nbsp;&nbsp; $n = (c_2 - c_1) / d$<br>
&nbsp;&nbsp; $n' = rotate90(n)$<br>

To find intersection points $p_1$ and $p_2$, the vector equations look like this:<br>

&nbsp;&nbsp; $p_1 = c_1 + n * (d + x) + n' * h$<br>
&nbsp;&nbsp; $p_2 = c_1 + n * (d + x) - n' * h$<br>

![Circle Intersection Points 12](https://github.com/user-attachments/assets/b5e44d25-f5c0-4cbe-b82b-99ab135277b2)

In total there are 2 square roots required. One to find distance $d$, and one to find $h$. You can also use $x$ and $h$ to find intersection area. You could get the **circle sector** area by using the ```Math.atan2()``` function and subtract the triangle area $A = h * (d + x)$ from it. You then do this for both circles and add the result together. More on this in a later explanation.
