There are two methods you can use to make an object frozen or unmovable. If the object is always going to be static, such as the ground, you can set it's mass to `0` when you create the mesh using the third parameter: `new Physijs.BoxMesh( geometry, material, 0 )`. Any object with a mass of `0` will always be static.

The second method can be used for objects when they will be static at some times and dynamic at others, like in the [jenga example](https://github.com/chandlerprall/Physijs/blob/master/examples/jenga.html#L166). If you call `object.setAngularFactor` and `object.setLinearFactor` with a `THREE.Vector3( 0, 0, 0 )` then no energy will be applied to the object. You can use `object.setAngularVelocity` and `object.setLinearVelocity` in the same way to clear any velocities the object may already have. At a later point you can reset the object's linear and angular factors to `( 1, 1, 1 )`, again as it's done in the [jenga example](https://github.com/chandlerprall/Physijs/blob/master/examples/jenga.html#L212).