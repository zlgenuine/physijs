Physijs currently supports 5 shapes:

* `Physijs.BoxMesh` - matches `THREE.CubeGeometry`
* `Physijs.SphereMesh` - matches `THREE.SphereGeometry`
* `Physijs.CylinderMesh` - matches `THREE.CylinderGeometry`
* `Physijs.ConeMesh` - matches `THREE.CylinderGeometry` (tapered)
* `Physijs.ConvexMesh` - matches any convex geometry you have

Using any of these shapes is as simple as replacing `THREE.Mesh` in your code with whatever Physijs mesh best suits your geometry. You add these meshes to the scene the same way you normally do, `scene.add( mesh_object )`.

There is one additional parameter you can pass to the `add` method: a callback. This callback function will be called when your mesh has been added to the physics simulation.

Look at the [shapes example](https://github.com/chandlerprall/Physijs/blob/master/examples/shapes.html) to see creating & adding shapes in action.