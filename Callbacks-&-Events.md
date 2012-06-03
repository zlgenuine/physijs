### Scene Update
Because Physijs runs on a different thread than your main application, there is no guarantee that it will be able to iterate the scene every time you call `scene.simulate`. Because of this, you may attach an event listener to the scene that is triggered whenever the physics simulation has run.

```javascript
var scene = new Physijs.scene;
scene.addEventListener( 'update', function() {
    // the scene's physics have finished updating
});
```

### Collisions
To be notified when an object experiences a collision with another object, you can attach a `collision` event listener to individual objects.

```javascript
var mesh = new Physijs.BoxMesh( geometry, material );
mesh.addEventListener( 'collision', function( other_object, linear_velocity, angular_velocity ) {
    // `this` is the mesh with the event listener
    // other_object is the object `this` collided with
    // linear_velocity and angular_velocity are floats representing the relative velocities of the impact
});
```

### Adding an object
If your scene is complex or has a lot of objects, the physics simulation can slow down to the point where adding new objects can become a lot of work for the application. To help alleviate some of the pain this may cause, objects have a `ready` event which is triggered after the object has been added to the physics simulation. This [can be seen](https://github.com/chandlerprall/Physijs/blob/master/examples/collisions.html#L150) in many of the examples in order to avoid flooding the scene with new objects as the simulation slows down.

```javascript
var readyHandler = function() {
    // object has been added to the scene
};
var mesh = new Physijs.SphereMesh( geometry, material );
mesh.addEventListener( 'ready', readyHandler );
scene.add( mesh );
```