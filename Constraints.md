### Point to Point
The point constraint allows objects to be bound to a certain point in the scene, and can be used to constrain two objects together at a point between them.

```javascript
var constraint = new Physijs.PointConstraint(
    physijs_mesh_a, // First object to be constrained
    physijs_mesh_b, // OPTIONAL second object - if omitted then physijs_mesh_1 will be constrained to the scene
    new THREE.Vector3( 0, 10, 0 ) // point in the scene to apply the constraint
);
scene.addConstraint( constraint );
```

### Hinge Constraint
The hinge constraint limits the movement of an object to act as if it were on a hinge, such as a door. Like the point constraint the hinge can be created with either 1 or 2 objects.

```javascript
var constraint = new Physijs.HingeConstraint(
    physijs_mesh_a, // First object to be constrained
    physijs_mesh_b, // OPTIONAL second object - if omitted then physijs_mesh_1 will be constrained to the scene
    new THREE.Vector3( 0, 10, 0 ), // point in the scene to apply the constraint
    new THREE.Vector3( 1, 0, 0 ) // Axis along which the hinge lies - in this case it is the X axis
);
scene.addConstraint( constraint );
constraint.setLimits(
    low, // minimum angle of motion, in radians
    high, // maximum angle of motion, in radians
    bias_factor, // applied as a factor to constraint error
    relaxation_factor, // controls bounce at limit (0.0 == no bounce)
);
constraint.enableAngularMotor( target_velocity, acceration_force );
constraint.disableMotor();
```


### Slider Constraint
The slider constraint will constrain the linear movement of an object to align with the given axis. Examples are a sliding door or the lifting mechanism on a fork lift. Like the point and hinge constraints, the second object is an optional parameter.

```javascript
var constraint = new Physijs.SliderConstraint(
    physijs_mesh_a, // First object to be constrained
    physijs_mesh_b, // OPTIONAL second object - if omitted then physijs_mesh_1 will be constrained to the scene
    new THREE.Vector3( 0, 10, 0 ), // point in the scene to apply the constraint
    new THREE.Vector3( 1, 0, 0 ) // Axis along which the hinge lies - in this case it is the X axis
);
scene.addConstraint( constraint );
constraint.setLimits(
    linear_lower, // lower limit of linear movement, expressed in world units
    linear_upper, // upper limit of linear movement, expressed in world units
    angular_lower, // lower limit of angular movement, expressed in radians
    angular_upper // upper limit of angular movement, expressed in radians
);
constraint.setRestitution(
    linear, // amount of restitution when reaching the linear limits
    angular // amount of restitution when reaching the angular limits
);
constraint.enableLinearMotor( target_velocity, acceration_force );
constraint.disableLinearMotor();
constraint.enableAngularMotor( target_velocity, acceration_force );
constraint.disableAngularMotor();
```


### ConeTwist Constraint
The cone twist constraint limits the movement and rotation between two objects in a manner similar to human joints like the shoulder or ankle. In this constraint both objects are required.

```javascript
var constraint = new Physijs.ConeTwistConstraint(
    physijs_mesh_a, // First object to be constrained
    physijs_mesh_b, // Second object to be constrained
    new THREE.Vector3( 0, 10, 0 ), // point in the scene to apply the constraint
);
scene.addConstraint( constraint );
constraint.setLimit( x, y, z ); // rotational limit, in radians, for each axis
constraint.setMotorMaxImpulse( max_impulse ); // float value of the maximum impulse the motor can apply toward its target
constraint.setMotorTarget( target ); // target is the desired rotation for the constraint and can be expressed by a THREE.Vector3, THREE.Matrix4, or THREE.Quaternion
constraint.enableMotor();
constraint.disableMotor();
```

### Degree Of Freedom Constraint
The degree of freedom constraint yields full control over how the object(s) should be constrained both in linear and angular movement.

```javascript
var constraint = new Physijs.DOFConstraint(
    physijs_mesh_a, // First object to be constrained
    physijs_mesh_b, // OPTIONAL second object - if omitted then physijs_mesh_1 will be constrained to the scene
    new THREE.Vector3( 0, 10, 0 ), // point in the scene to apply the constraint
);
scene.addConstraint( constraint );
constraint.setLinearLowerLimit( new THREE.Vector3( -10, -5, 0 ) ); // sets the lower end of the linear movement along the x, y, and z axes.
constraint.setLinearUpperLimit( new THREE.Vector3( 10, 5, 0 ) ); // sets the upper end of the linear movement along the x, y, and z axes.
constraint.setAngularLowerLimit( new THREE.Vector3( 0, -Math.PI, 0 ) ); // sets the lower end of the angular movement, in radians, along the x, y, and z axes.
constraint.setAngularUpperLimit( new THREE.Vector3( 0, Math.PI, 0 ) ); // sets the upper end of the angular movement, in radians, along the x, y, and z axes.
constraint.configureAngularMotor(
    which, // which angular motor to configure - 0,1,2 match x,y,z
    low_limit, // lower limit of the motor
    high_limit, // upper limit of the motor
    velocity, // target velocity
    max_force // maximum force the motor can apply
);
constraint.enableAngularMotor( which ); // which angular motor to configure - 0,1,2 match x,y,z
constraint.disableAngularMotor( which ); // which angular motor to configure - 0,1,2 match x,y,z
```