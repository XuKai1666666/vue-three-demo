<script  setup lang="ts">
import * as THREE from 'three'
import { onMounted } from 'vue'
import { MMDLoader } from 'three/examples/jsm/loaders/MMDLoader'
//引入轨道控制器（用来通过鼠标事件控制模型旋转、缩放、移动），没有这个需求可不引入
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import Menu from './Menu.vue'
const scene = new THREE.Scene()
const width = window.innerWidth, height = window.innerHeight,
	camera = new THREE.PerspectiveCamera(45, width / height, 1, 1000)
//添加光源 这里添加了两个光源
//AmbientLight：环境光源，均匀照亮所有物体，防止有些光源照射不到呈现不出来
//PointLight：点光源，类似灯泡发出的光，可以投射阴影，使模型更加立体
const ambientLight = new THREE.AmbientLight(0xffffff, 0.5)
const pointLight = new THREE.PointLight(0xffffff, 0.4)
//设置点光源所在位置
pointLight.position.set(200, 300, 400)
//每创建一个object都需要将其添加到三维场景中
scene.add(ambientLight)
scene.add(pointLight)
scene.background = new THREE.Color(0x3b5556);
camera.position.set(90, -50, -50)
camera.lookAt(100, 100, 100)

// const geometry = new THREE.BoxGeometry(100, 100, 100)
// //创建材质（外观）
// const material = new THREE.MeshLambertMaterial({
//     color: 0x00ffff,//设置材质颜色
//     transparent: true,//开启透明度
//     opacity: 0.5 //设置透明度
// })
// //创建一个网格模型对象,将上面设置好的物体及其材质注入到模型对象中
// const mesh = new THREE.Mesh(geometry, material)
// // console.log('getWorldScale  '+mesh.getWorldScale(scene));
// mesh.scale
// console.log('scale  '+mesh.scale);
// scene.add(mesh)

const renderer = new THREE.WebGLRenderer({ antialias: true })


// Instantiate a loader
const loader = new MMDLoader();
// Load a MMD model
loader.load(
	// path to PMD/PMX file
	'src/assets/keli/可莉2.0.pmx',
	// called when the resource is loaded
	function (mesh) {
		mesh.scale.set(3, 3, 3);
		scene.add(mesh);
		renderer.setSize(width, height)
		renderer.render(scene, camera)
	},

	function (xhr) {

		console.log((xhr.loaded / xhr.total * 100) + '% loaded');

	},
	// called when loading has errors
	function (error) {

		console.log('An error happened');

	}
);

onMounted(() => {
	//将渲染器绘制出的canvas添加到页面中
	document.getElementById('keli')?.appendChild(renderer.domElement)
})
//创建轨道控制器
const controls = new OrbitControls(camera, renderer.domElement)
//添加事件监听 当事件发生改变时触发
controls.addEventListener('change', () => {
	//重新渲染
	renderer.render(scene, camera)
})
</script>
<template>
	<div id="keli" ><div id="menu" ><Menu/></div></div>
	
</template>

<style>
	div{
		overflow: hidden;
		position: fixed;
	}
#menu{
	right: 500px;
	top: 100px;
}
#keli{
	float: left;
}
</style>