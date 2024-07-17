<i><b>Required knowledge:</b>
- [getting area of a triangle](https://github.com/WMaster7/GameMath/tree/main/Intermediate/Calculate%20Triangle%20Area) (signed, depening on winding)</i>

## Check if a Point is inside a Triangle

Knowing if a point is inside a triangle can be done with comparing triangle shaped areas with eachother. We will have a total of 4 points, points $a$ $b$ and $c$ for the triangle, and point $p$ as our point to check.<br>

Since we're only going to compare areas, we can **ommit the division by 2** part for getting the area of a triangle, since all terms would have this and we do not need the precise area value. Recalling our simple area formula, where $ab'$ is vector $ab$ rotated by 90 degrees Counter-Clockwise.<br>

&nbsp;&nbsp; $A_{tri} = dot(ab', bc)$<br>
