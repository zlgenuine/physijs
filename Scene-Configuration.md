When creating the scene there are a few choices you can make. Most of these are passed to the scene when you create it:

```javascript
var scene = new Physijs.Scene({ reportsize: 50, fixedTimeStep: 1 / 60 });
```

### Scene constructor parameters
* **fixedTimeStep** `default 1 / 60` *This number determines how much time one simulation step is to simulate. The small the number the more accurate (and slow) the simulation.*
* **broadphase** `default dynamic` *Specifies which broadphase will be used, choices are `dynamic` and `sweepprune`.*
* **reportsize** `default 50` *As an optimization, world reports which contain object positions are pre-initialized based on this number. It's best to set this to the number of objects your scene will have.*

### Scene configuration methods
* **setGravity** `default ( 0, -10, 0 )` *Method which sets the amount and direction of gravitational forces. Usage: `scene.setGravity(new THREE.Vector3( x_force, y_force, z_force ))`*

### Custom simulation steps
There are two parameters you can pass to the `scene.simulate` method: `timeStep` and `maxSteps`. `timeStep` specifies the amount of time to be simulated and defaults to the amount of time since the last iteration. `maxSteps` is an upper limit of the number of iterations the simulation may perform. ***The amount of time the simulator is told to run (`timeStep`) can be limited by the number of iterations allowed (`maxSteps`).*** For example:

If `fixedTimeStep` (see above) is `1 / 60` (`16` milliseconds) and `maxSteps` is 5, the max time that can be simulated is `maxSteps` * `fixedTimeStep` = 0.08 seconds, or 80 milliseconds. If a `timeStep` less than or equal to 80ms is given, everything will be simulated, but if `timeStep` exceeds 80ms then not all of the time will be simulated. In this way `maxSteps` can be used to prevent the physics simulation from grinding to a complete halt if it starts getting overloaded. In the examples `scene.simulate` is called with parameters of `( undefined, 2 )` which tells Physijs to simulate as much as possible up to 2 iterations.