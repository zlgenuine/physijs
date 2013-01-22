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

See the [collisions example](https://github.com/chandlerprall/Physijs/blob/master/examples/collisions.html) for details on implementing and using this event.

### Motion Clamping

When an object has a high velocity, collisions can be missed if it moves through and past other objects between simulation steps. To fix this, enable CCD motion clamping. For a cube of size 1 try:

```javascript
// Enable CCD if the object moves more than 1 meter in one simulation frame
mesh.setCcdMotionThreshold(1);

// Set the radius of the embedded sphere such that it is smaller than the object
mesh.setCcdSweptSphereRadius(0.2);
```

See the [Bullet wiki page on motion clamping] for more information.

### Future Plans

In the future a global collision report will be sent to the scene's `update` event.


[Bullet wiki page on motion clamping]: http://www.bulletphysics.org/mediawiki-1.5.8/index.php/Anti_tunneling_by_Motion_Clamping