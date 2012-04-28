You can use Physijs without ever touching its materials system. However, in doing so you would not be able to customize how much friction and restitution ("bounciness") objects have.

Materials are super easy to use but take a little getting used to. You must call `Physijs.createMaterial` with the three.js material, friction, and restitution values you want the Physijs material to have. This new material can be used just like any other three.js material.

**Note: friction and restitution values are given between 0.0 and 1.0**

```javascript
var friction = .8; // high friction
var restitution = .3; // low restitution

var material = Physijs.createMaterial(
    new THREE.MeshBasicMaterial({ color: 0x888888 }),
    friction,
    restitution
);

// Create a cube with friction of .8 and restitution of .3
var mesh = new Physijs.BoxMesh(
    new THREE.CubeGeometry( 5, 5, 5 ),
    material
);
```