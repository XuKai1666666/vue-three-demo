<script  setup lang="ts">
import * as THREE from 'three' 
import { onMounted  } from 'vue'
import {MMDLoader} from 'three/examples/jsm/loaders/MMDLoader'
const scene = new THREE.Scene()
const width = window.innerWidth, height = window.innerHeight  ,
      camera = new THREE.PerspectiveCamera(45, width/height, 1, 1000)
camera.position.set(200,200,200) 
camera.lookAt(0,0,0)
 // Instantiate a loader
const loader = new MMDLoader();
THREE.DefaultLoadingManager
// Load a MMD model
loader.load(
	// path to PMD/PMX file
	'src/assets/可莉/可莉2.0.pmx',
	// called when the resource is loaded
	function ( mesh ) {

		scene.add( mesh );

	},
	// called when loading is in progresses
	function ( xhr ) {

		console.log( ( xhr.loaded / xhr.total * 100 ) + '% loaded' );

	},
	// called when loading has errors
	function ( error ) {

		console.log( 'An error happened' );

	}
);

</script>
<template>
    <div id="keli"></div>
</template>