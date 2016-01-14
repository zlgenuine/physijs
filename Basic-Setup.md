The primary goal in developing Physijs is to keep it as simple and user-friendly as possible. Physics engines can be daunting and difficult to set up, with so many options and configurations it is easy to feel overwhelmed. Physijs abstracts all of that extra logic out so you can focus on the rest of your project.

It is a plugin for [three.js](https://github.com/mrdoob/three.js), a great noob-friendly WebGL framework. As such, you need to use three.js for your scene management in order to use Physijs. If you're not familiar with three.js then spend a couple of days learning it and come back; if you know the basics of three.js then you already know the basics of Physijs as well.

How do you add Physijs to your project? In just six simple steps:

* Add the `<script>` tag to your page and point it at the `physi.js` file.
* Configure the `Physijs.scripts.worker` and `Physijs.scripts.ammo` Javascript parameters to point at the web worker and Ammo.js scripts
* Use `Physijs.Scene` in place of `THREE.Scene`
* Instead of `THREE.Mesh`, select the best physics mesh such as `Physijs.BoxMesh`, `Physijs.SphereMesh`, or `Physijs.ConvexMesh`
* Call the `scene.simulate` method when you render or whenever you want to iterate the physics setup.

Below you will see a very basic scene that results in a cube falling down out of view. In all, it only took 4 lines of new code and 2 modified lines to give a three.js scene some physics.

Take a look at the [included examples](https://github.com/chandlerprall/Physijs/tree/master/examples) to see what Physijs can do.

**NOTE** because Physijs runs in a separate thread from your main application it is entirely possible to call `scene.simulate` while a previous simulation call is running. When this happens, `scene.simulate` will return `false`.

```html
<!DOCTYPE html>
<html>

<head>
	<script type="text/javascript" src="/js/Three.js"></script>
	<script type="text/javascript" src="/js/physi.js"></script>
	
	<script type="text/javascript">
	
	'use strict';
	
	Physijs.scripts.worker = '/js/physijs_worker.js';
	Physijs.scripts.ammo = '/js/ammo.js';
	
	var initScene, render, renderer, scene, camera, box;
	
	initScene = function() {
		renderer = new THREE.WebGLRenderer({ antialias: true });
		renderer.setSize( window.innerWidth, window.innerHeight );
		document.getElementById( 'viewport' ).appendChild( renderer.domElement );
		
		scene = new Physijs.Scene;
		
		camera = new THREE.PerspectiveCamera(
			35,
			window.innerWidth / window.innerHeight,
			1,
			1000
		);
		camera.position.set( 60, 50, 60 );
		camera.lookAt( scene.position );
		scene.add( camera );
		
		// Box
		box = new Physijs.BoxMesh(
			new THREE.CubeGeometry( 5, 5, 5 ),
			new THREE.MeshBasicMaterial({ color: 0x888888 })
		);
		scene.add( box );
		
		requestAnimationFrame( render );
	};
	
	render = function() {
		scene.simulate(); // run physics
		renderer.render( scene, camera); // render the scene
		requestAnimationFrame( render );
	};
	
	window.onload = initScene();
	
	</script>
</head>

<body>
	<div id="viewport"></div>
</body>
</html>
```