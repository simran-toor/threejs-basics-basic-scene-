BASIC SCENE 
	- make Three.js work the simplest possible way
	- no bundler, no modules, no dependencies 
	- A JavaScript and a HTML file

CREATING FILES 
	 1. create plain index.html file 
	 	1.1 ! to give skeleton 
	 	1.2 add script tag for js file 
	 		<script src="./script.js"></script>
	 2. create script.js file 
		2.1 in script.js console.log("hello") to check it works 
	 3. download threejs master file, unzip 
	 	3.1 copy three.min.js file from master folder into project folder 
	 4. load into html file by adding script tag before script.js file (b/c you need to load library to able to use in script.js file)

HOW TO USE THREE.JS
	The THREE variable 
		- contains most of the classes and properties but not all 
		- Log it in the console with console.log(THREE)
		- always use uppercase 

4 ELEMENTS TO GET STARTED 
	- a scene that will contain objects
	- some objects
	- a camera
	- a renderer  
	
SCENE 
	- like a container 
	- we put objects, models, lights etc. in it 
	- at some point we ask Three.js to render that scene 
	5. in script.js 
		const scene = new THREE.Scene()

OBJECTS
	- primitive geometries 
	- imported models 
	- particles 
	- lights etc. 

SIMPLE RED CUBE 
	6. CREATE A MESH
		- combination of a geometry and a material 
		- start with BoxGeometry and a MeshBasicMaterial
			const geometry = new THREE.BoxGeometry(1, 1, 1)
		- the first 3 parameters correspond to the box's size
	7. MATERIAL
		const material = new THREE.MeshBasicMaterial({ color: '0xff0000'})
	
	8. MESH
		const mesh = new THREE.Mesh(geometry, material);
	
	9. ADD TO SCENE 
		- using add(…) method 
			scene.add(mesh);
	
	10. CAMERA
		- not visible 
		- serves as point of view when doing a render
		- can have multiple and switch between them 
		- different types 
		- use PerspectiveCamera 
			const camera = new THREE.PerspectiveCamera();
				- needs 2 parameters:
					1. THE FIELD OF VIEW
						- vertical vision angle
						- in degrees 
						- aka fov 
							const camera = new THREE.PerspectiveCamera(75);
					2. THE ASPECT RATIO 
						- the width of the render divided by the height of the render 
						10.1 create sizes object containing temp values (before camera)
								const sizes = {
								    width: 800,
								    height: 600
								};
						10.2 add aspect ratio to camera 
							const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height);
		10.3 add camera to scene 
			scene.add(camera)
	
	11. RENDERER
		- render the scene from the camera point of view 
		- results drawn into a canvas
		- a canvas is a HTML element in which you can draw stuf 
		- Three.js will use WebGL to draw the render inside this canvas 
		- you can create it or you can let Three.js do it 
		11.1 create the <canvas> element before you load thes cripts with a webgl class
			- in index.html body 
				    <canvas class="webgl"></canvas>
		11.2 create WebGLRenderer with an empty object 
			- in script.js 
				const renderer = new THREE.WebGLRenderer({})
		11.3 use document.querySelector(...) to retrieve the canvas created in HTML and store it in a canvas variable
			const canvas = document.querySelector('.webgl');
		11.4 add canvas to renderer object 
			const renderer = new THREE.WebGLRenderer({
			    canvas: canvas
			})
				- if property name is the exact same as variable name code can be shortened to: 
					const renderer = new THREE.WebGLRenderer({
					    canvas
					})
		11.5 resize renderer using setSize(...)
			renderer.setSize(sizes,width, sizes.height);
	
	12. FIRST RENDER
		- call the renderer(...) method on the renderer with scene and the camera as parameters
			renderer.render(scene, camera)
		12.1 nothing is visible b/c the camera is inside the cube, so need to move camera backward
			- to transform an object, use the following properties:
				- position
					- this property is also an object with x, y and z properties 
					- three.js considers forward/backward axis to be z 
				- rotation 
				- scale
			- move camera backward before doing the render 
			- before scene.add(camera)
				camera.position.z = 3;
