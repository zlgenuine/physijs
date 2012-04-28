Compound shapes are an efficient way to add complex geometry to the scene and are created by piecing together the [available shapes](https://github.com/chandlerprall/Physijs/wiki/Basic-Shapes) in Physijs to create a larger, more intricate geometry.

In three.js you would add these child geometries together by adding them to the parent objects, for example:

```javascript
var parent = new THREE.Mesh( new THREE.CubeGeometry( 5, 5, 5 ), new THREE.MeshBasicMaterial({ color: 0x888888 }) );

var child = new THREE.Mesh( new THREE.SphereGeometry( 2.5 ), new THREE.MeshBasicMaterial({ color: 0x888888 }) );
child.position.z = 5;

parent.add( child );
scene.add( parent );
```

The above code would create a 5x5x5 cube and attach a 2.5 radius sphere to it 5 units away on the z axis. Moving and rotating the parent object directly affects the child. In order to keep the Physijs plugin simple and uncomplicated this is **exactly** how its compound shapes work. The only change needed is to replace `THREE.Mesh` with the Physijs equivalents:

```javascript
var parent = new Physijs.BoxMesh( new THREE.CubeGeometry( 5, 5, 5 ), new THREE.MeshBasicMaterial({ color: 0x888888 }) );

var child = new Physijs.SphereMesh( new THREE.SphereGeometry( 2.5 ), new THREE.MeshBasicMaterial({ color: 0x888888 }) );
child.position.z = 5;

parent.add( child );
scene.add( parent );
```

The only thing you need to remember when working with compound objects is **all** children **must** be added to the parent before the parent is added to the scene. When a parent is put into the scene its shape is finalized and cannot be added to.

Look at the [compound shapes](https://github.com/chandlerprall/Physijs/blob/master/examples/compound.html) example for more details on this implementation.