Fraction of work

Porwal 1/3
Romani 1/3
Zaninelli 1/3

--- Phong Lighting Model and Shadows ---
First of all we computed the ambient light contribution to the current point, using the ambience light intensity multiplied by the material's ambient reflection coefficient.

Then we iterated over all light sources: for each of them we computed the ray that connects the considered point with the current source and checked that it does not have any intersection a part from the point itself. To do this, we first slightly shifted the point towards the light source, to avoid numerical errors. 
In case no intersections occured, we added the diffusive and specular contributions if the condition of illumination were satisfied (dot(normal,l) >= 0 and dot(r,view) >= 0, where l is the direction of the ray we created and r is its reflection with respect to the normal). 

--- Reflections ---
For this part, we first compute its color (c1) with the function lighting. Then we checked that the material had reflection coefficient different from 0 and, in this case, we created the reflected ray and recursively call the function trace to get the final color. This is given by (1-alpha)*c1 + alpha*c2 where c2 is the color returned by the recursion. We stop the recursion either if we do not intersect any object with a ray, or if we reach a maximum number of secondary rays (max_depth).
