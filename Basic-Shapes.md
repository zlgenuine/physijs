Physijs currently supports 9 shapes:

* `Physijs.PlaneMesh` - infinite zero-thickness plane
* `Physijs.BoxMesh` - matches `THREE.CubeGeometry`
* `Physijs.SphereMesh` - matches `THREE.SphereGeometry`
* `Physijs.CylinderMesh` - matches `THREE.CylinderGeometry`
* `Physijs.ConeMesh` - matches `THREE.CylinderGeometry` (tapered)
* `Physijs.CapsuleMesh` - matches `THREE.CylinderGeometry`, except has two half spheres at ends
* `Physijs.ConvexMesh` - matches any convex geometry you have
* `Physijs.ConcaveMesh` - matches any concave geometry you have, i.e. arbitrary mesh
* `Physijs.HeightfieldMesh` - matches a regular grid of height values given in the z-coordinates

Using any of these shapes is as simple as replacing `THREE.Mesh` in your code with whatever Physijs mesh best suits your geometry. You add these meshes to the scene the same way you normally do, `scene.add( mesh_object )`.

Look at the [shapes example](https://github.com/chandlerprall/Physijs/blob/master/examples/shapes.html) to see creating & adding shapes in action.

### Notes

* Use `Physijs.ConcaveMesh` sparingly, it has the worst performance
* `THREE.PlaneMesh` and `Physijs.PlaneMesh` are not strictly analogous as the latter is infinite. A very thin BoxMesh can better represent finite planes.
* `Physijs.CapsuleMesh` is usually good for humanoid player characters