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