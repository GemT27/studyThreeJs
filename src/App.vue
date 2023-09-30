<script setup>
// 引入threeJs
import * as THREE from 'three';
// 轨道控制器
import {OrbitControls} from "three/addons/controls/OrbitControls.js";

// 创建一个三维场景scene
const scene = new THREE.Scene();

// 给三维场景添加物体

// 定义一个几何体，长宽高都为100
const geometry = new THREE.BoxGeometry(100, 100, 100);

// 创建一个材质对象
const material = new THREE.MeshLambertMaterial({
  color: 'red',
});

const light = new THREE.PointLight('white', 1.0);
light.position.set(300, 200, 150);
// scene.add(light);

// 可视化点光源
const pointLightHelper = new THREE.PointLightHelper(light, 10);
// scene.add(pointLightHelper);

// 添加环境光
const ambient = new THREE.AmbientLight('white', 1);
// scene.add(ambient);

// 添加一个平行光
const directionalLight = new THREE.DirectionalLight('white', 1);
directionalLight.position.set(50, 100, 60)
scene.add(directionalLight);

// 可视化平行光
const pointLightHelper2 = new THREE.DirectionalLightHelper(directionalLight, 20, 'red');
scene.add(pointLightHelper2);


// 创建一个网格模型，表示生活中的物体
const mesh = new THREE.Mesh(geometry, material);
mesh.position.set(0, 0, 0);
// 将mesh物体添加到场景中
scene.add(mesh);

// 创建三维坐标轴
const axesHelper = new THREE.AxesHelper(200);
scene.add(axesHelper);


// 创建一个相机camera透视投影
const width = 800;
const height = 500;
const camera = new THREE.PerspectiveCamera(50, width / height, 0.1, 2000);

// 设置相机的位置
camera.position.set(200, 200, 200);
camera.lookAt(0, 0, 0);

// 创建一个渲染器对象
const renderer = new THREE.WebGLRenderer();
renderer.setSize(width, height);
renderer.render(scene, camera);

document.body.appendChild(renderer.domElement);

// 创建一个相机控件对象
const controls = new OrbitControls(camera, renderer.domElement);

controls.addEventListener('change', () => renderer.render(scene, camera));

// 周期性执行, 理想状态下
const clock = new THREE.Clock();
const render = () => {
  const spt = clock.getDelta() * 1000;
  requestAnimationFrame(render)
  mesh.rotateY(0.01)
  renderer.render(scene, camera)
}

render()
</script>

<template>
</template>

<style scoped>

</style>
