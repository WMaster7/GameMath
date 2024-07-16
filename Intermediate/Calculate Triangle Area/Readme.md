<i><b>Required knowledge:</b>
- vectors
- getting vector lengths
- rotating vector 90 degrees
- unit vectors
- dot product</i>

## Calculate Triangle Area

![Triangle Area Formula](https://github.com/user-attachments/assets/1590d4f6-6702-41f2-9c13-96c009403951)

Quick reminder: $A = \frac{b\times h}{2}$<br>
The formula for the area of a triangle is half of its base times its height.<br>

We can also get it with 3 arbitrary 2D points with a simple formula, which is much more useful on computers.<br>

Start by creating 2 vectors $ab$ and $bc$.

![Triangle Area Step 01](https://github.com/user-attachments/assets/e8050e9c-8af0-428f-8d82-d6efa1f33509)

For this example let $ab$ be the base.<br>
Now we need the height, which is perpendicular to the base. We can rotate $ab$ by 90 degrees to get this direction as $ab'$.<br>
If we normalize $ab'$ and apply the dot product with vector $bc$, we get the length of $bc$ along the perpendicular, which would be our height $h$.

![Triangle Area Step 02](https://github.com/user-attachments/assets/083239a4-3af1-4411-8e52-8d5eaf1626f8)

Normalizing requires an **expensive square root fuction**, which is not ideal, so lets simplify.<br>

Let $base = length(ab)$<br>
And $height = dot(normalize(ab'), bc)$<br>
Recall that $normalize(ab') = ab'/length(ab)$<br>

Because the division by $length(ab)$ happens for both $x$ and $y$, our dot product will look like this:<br>

&nbsp;&nbsp; $ab'.x/length(ab)\times bc.x + ab'.y/length(ab)\times bc.y$<br>

Multiplying by $base$ to get $base\times height$ eliminates the division by $length(ab)$.<br>

&nbsp;&nbsp; $ab'.x\times bc.x + ab'.y\times bc.y$<br>

Which is simply the dot product of $ab'$ with $ac$. So our final result:<br>

&nbsp;&nbsp; $A = dot(ab', bc)/2$

This is all we need to get the area! This is computationally fast and only requires to rotate one of its vectors by 90 degrees. This is all done with additions, subtractions and scaling. If it's really critical code, you could even try to ommit the vector components and only use the points. That would look something like this:<br>
```
ab = (b.x-a.x, b.y-a.y)
ab' = (a.y-b.y, b.x-a.x)
bc = (c.x-b.x, c.y-b.y)
dot(ab',bc) = (a.y-b.y)*(c.x-b.x) + (b.x-a.x)*(c.y-b.y)
= (a.y*c.x)-(a.y*b.x)-(b.y*c.x)+(b.y*b.x)+(b.x*c.y)-(b.x*b.y)-(a.x*c.y)+(a.x*b.y)
= (a.y*c.x)-(a.y*b.x)-(b.y*c.x)+(b.x*c.y)-(a.x*c.y)+(a.x*b.y)
```

&nbsp;&nbsp; $2A = (a.y\times c.x)-(a.y\times b.x)-(b.y\times c.x)+(b.x\times c.y)-(a.x\times c.y)+(a.x\times b.y)$<br>

**Note:** that the area can actually be negative depending on which vector was rotated and to which side. This actually becomes useful with other algorithms. To get a positive result, either know that the points are sorted in the same direction as the rotation for $ab'$ (Counter-Clockwise with Counter-Clockwise) or simply use the ```Math.Abs()``` function to turn any negative into a positive number.
