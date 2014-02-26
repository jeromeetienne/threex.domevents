threex.suzanne
==============

It is a 
[threex](http://jeromeetienne.github.io/threex/) extension 
for 
[three.js](http://threejs.org)
which provide you a monkey model.
This is the blender famous suzanne.

Show Don't Tell
===============
* [examples/basic.html](http://jeromeetienne.github.io/threex.suzanne/examples/basic.html)
\[[view source](https://github.com/jeromeetienne/threex.suzanne/blob/master/examples/basic.html)\] :
It shows a basic usage of the extension.

How To Install It
=================

You can install it via script tag

```html
<script src='threex.suzanne.js'></script>
```

Or you can install with [bower](http://bower.io/), as you wish.

```bash
bower install threex.suzanne
```

How To Use It
=============

### How to load the geometry ?

```javascript
new THREEx.Suzanne.GeometryLoader(function onLoad(geometry){
	// this function is notified when the geometry is actually loaded
	
	// geometry is a THREE.Geometry of suzanne model
})
```

### How to create a mesh with it ?

```javascript
new THREEx.Suzanne.GeometryLoader(function onLoad(geometry){
	// create a mesh with the geometry
	var material	= new THREE.MeshNormalMaterial()
	var mesh	= new THREE.Mesh( geometry, material )
	// attach mesh to the scene
	scene.add(mesh)
})
```

Sometime it is not desirable to wait for the loading to complete before 
adding the object to the scene. To avoid this, we create a container
which will contains the model once loading is completed.
Thanks to the scene graph inheritance, any position/quaternion/scale
changes made on container, will be reported to the children meshes.

```javascript
// create the container
var container	= new THREE.Object3D();
// add the container to the scene without waiting the end of loading
scene.add(container)
// start to load the geometry
new THREEx.Suzanne.GeometryLoader(function onLoad(geometry){
	// create a mesh with it
	var material	= new THREE.MeshNormalMaterial()
	var mesh	= new THREE.Mesh( geometry, material )
	// attach mesh to the container
	container.add(mesh)
})
```
