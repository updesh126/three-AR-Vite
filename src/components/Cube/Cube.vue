<script setup>
import { ref, onMounted} from 'vue';
import * as THREE from 'three';

let scene = new THREE.Scene();

let canvasRef = ref();
let renderer;

let boxGeometry = new THREE.BoxGeometry(1,1,1);
let boxMaterial = new THREE.MeshStandardMaterial({color: "mediumpurple"});

let box = new THREE.Mesh(boxGeometry, boxMaterial);
box.position.set(0,0,-2);
scene.add(box);

const ambientLight = new THREE.AmbientLight( "#ffffff" , 1); // soft white light
scene.add( ambientLight );

let camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight,0.1, 100);

camera.position.y =1;
camera.position.z = 2;
camera.lookAt( new THREE.Vector3(0,0,0));


scene.add(camera);

onMounted(() => {
    renderer = new THREE.WebGLRenderer({
        canvas: canvasRef.value,
        antialias: true,
        alpha: true,
    })
    renderer.setSize(window.innerWidth, window.innerHeight);
    // renderer.setClearColor(0x000000, 1);
    renderer.setPixelRatio(window.devicePixelRatio)

    renderer.render(scene,camera)
   
});

</script>

<template>
    <canvas ref="canvasRef"></canvas>
</template>