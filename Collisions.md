Collisions are currently handled with object-level collision events. These events pass 3 parameters: the other object being collided with, the difference in velocity between the two objects (essentially the speed of impact), and the difference in angular velocity.

```javascript
var mesh = new Physijs.SphereMesh(
    new THREE.SphereGeometry( 3 ),
    new THREE.MeshBasicMaterial({ color: 0x888888 })
);
mesh.addEventListener( 'collision', function( other_object, relative_velocity, relative_rotation ) {
    // `this` has collided with `other_object` with an impact speed of `relative_velocity` and a rotational force of `relative_rotation`
});
```

In the future a global collision report will be sent to the scene's `update` event.

See the [collisions example](https://github.com/chandlerprall/Physijs/blob/master/examples/collisions.html) for details on implementing and using this event.