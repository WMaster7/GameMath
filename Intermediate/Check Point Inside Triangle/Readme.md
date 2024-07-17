<i><b>Required knowledge:</b>
- [getting area of a triangle](https://github.com/WMaster7/GameMath/tree/main/Intermediate/Calculate%20Triangle%20Area) (signed, depening on winding)</i>

## Check if a Point is inside a Triangle

Knowing if a point is inside a triangle can be done with comparing triangle shaped areas with eachother. We will have a total of 4 points, points $a$ $b$ and $c$ for the triangle, and point $p$ as our point to check.<br>

Since we're only going to compare areas, we can **ommit the division by 2** part for getting the area of a triangle, since all terms would have this and we do not need the precise area value. Recalling our simple area formula, where $ab'$ is vector $ab$ rotated by 90 degrees Counter-Clockwise.<br>

&nbsp;&nbsp; $A_{tri} = dot(ab', bc)$<br>

Lets pick a triangle with points in Counter-Clockwise order (also known as winding).

![Point Inside Triangle Step 01](https://github.com/user-attachments/assets/9d1fcbe7-aea8-485f-bfaa-c6dde09c2dbb)

With point $p$, we can create 2 triangles and get their areas as $A_1$ for triangle $abp$ and $A_2$ for triangle $apc$.

![Point Inside Triangle Step 02](https://github.com/user-attachments/assets/5544bc0a-97c4-483b-937c-10bd07d68a3b)

Areas $A_1$ and $A_2$ combined will be less than $A$ if $p$ is within the triangle, and greater if $p$ reaches beyond segment $bc$.

![Point Inside Triangle Step 03](https://github.com/user-attachments/assets/41945510-83f8-4397-97c4-144a0ec9172f)

So our first condition will be: ```(A1 + A2) <= A``` which can also be written as ```(A1 + A2 - A) <= 0```<br>

As point $p$ reaches beyond line $ac$, the winding changes and $A_2$ becomes negative. Similarly for $A_1$ when $p$ reaches beyond $ab$.<br>
To restrain point $p$ within the triangle, both $A_1$ and $A_2$ must not be negative.

![Point Inside Triangle Step 04](https://github.com/user-attachments/assets/a5f1768d-a054-4dca-ac0a-b6241b980ddb)&nbsp;&nbsp;&nbsp;&nbsp;![Point Inside Triangle Step 05](https://github.com/user-attachments/assets/d689aacb-8675-406c-99c7-b4d662357b6a)

Giving additional conditions of ```A1 >= 0``` and ```A2 >= 0```<br>

It's important to note that all areas will be inverted when $abc$ happens to have another winding, making all conditions incorrect. In some situations it can therefore be useful to know or keep a certain winding.

![Point Inside Triangle Step 06](https://github.com/user-attachments/assets/beb715d5-94ec-4492-aad6-7b9aa65722ac)

If keeping a certain winding is not an option, you can check the winding of $abc$ by getting the sign of its area $S = sign(A)$ and multiplying each area component by that sign.<br>

```
A = triArea(a, b, c)
A1 = triArea(a, b, p)
A2 = triArea(a, p, c)

// For unknown winding
S = Math.Sign(A)
inside = ((A1 + A2 - A) * S) <= 0f
      && (A1 * S) >= 0f
      && (A2 * S) >= 0f

// For known winding
inside = (A1 + A2 - A) <= 0f
    && A1 >= 0f
    && A2 >= 0f
```

In general these formulas hold for proper triangles. If 3 points form not any triangle by being on the same line, all conditions will only be satisfied when $p$ is on that line, but without restraint in length.<br>
To combat this behaviour, you may check if $A$ is zero and return ```false``` or return any other result like checking if $p$ is on segment $ab$ or $bc$.<br>
You may also choose to not count borders as being inside by replacing ```<=``` with ```<``` and ```>=``` with ```>```. This also eliminates the case where $abc$ is not a proper triangle volume.

### Concluding

This solution is quite simple and probably fast to execute, as getting an area can be done with just a dot product.
