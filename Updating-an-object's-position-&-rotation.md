There is one aspect where a seamless integration with three.js could not be done: changing an object's position and/or rotation. If you do so, you must set that object's `__dirtyPosition` or `__dirtyRotation` flag to `true`, otherwise it will be overwritten from the last known values in the simulation.

```javascript
var mesh = new Physijs.BoxMesh( geometry, material );
scene.add( mesh );

var render = function() {
    // Change the object's position
    mesh.position.set( 0, 0, 0 );
    mesh.__dirtyPosition = true;
    
    scene.simulate();
    renderer.render();
};
```