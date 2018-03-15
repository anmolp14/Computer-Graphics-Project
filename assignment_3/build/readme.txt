Fraction of work

Porwal 1/3
Romani 1/3
Zaninelli 1/3

Vertex Normals
In this part we needed to compute normal for each vertex; this is done iterating over all the triangles of the mesh and first computing the angleWeights of the current triangle and then, for each of its vertices we added the contribution to the normal given by the considered triangle (the contribution is given by the angleWeight * the normal of the triangle, as in the formula). In the end we normalized the normal of every vertex.

Ray-triangle intersection
We rewrote the system as
(p0-p2)*alpha + (p1-p2)*beta -d*t = o - p2
Then we created a lambda function to compute the determinant of a 3x3 matrix which is needed to implement the Cramer's rule.
Then we checked that the barycenter coordinates were positive and that the intersection was in front of the viewer: in this case we assigned the _intersection_t, intersection_point and the intersection_normal according to the draw_mode (FLAT -> assign the triangle normal, PHONG -> interpolate the vertex normals).

Efficient Ray-Mesh Intersections
We first computed the intersections with the two planes orthogonal to the x direction passing through the points bb_min_ and bb_max_, assigning the values of tmin and tmax in such a way that tmin <= tmax.
We did the same for the plane orthogonal to the y direction and assigned the values tymin and tymax. We checked if these 2 set of points intersect with the box by checking whether (tmin < tymax) && (tymin < tmax). In this case we did the same for the z component.

