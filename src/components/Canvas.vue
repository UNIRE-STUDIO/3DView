<script>
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import GameLoop from '@/scripts/gameLoop';
import { render } from 'vue';

export default {
    mounted() {
        // Сцена
        const scene = new THREE.Scene();
        const canvas = document.querySelector('.canvas');

        // Камера
        const sizes = {
            width: 500,
            height: 500,
        };

        const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height);
        camera.position.z = 3;
        const controls = new OrbitControls(camera, canvas);
        scene.add(camera);

        // Объект
        // const geometry = new THREE.BoxGeometry(1, 1, 1);
        // const material = new THREE.MeshBasicMaterial({
        //     color: 'yellow',
        //     wireframe: true,
        // });
        //const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });


        const pointLight = new THREE.PointLight(0xffffff, 5, 10);
        pointLight.position.set(2, 2, 0)
        scene.add(pointLight)

        const gltfLoader = new GLTFLoader();
        let model;
        gltfLoader.load('/models/model.glb', (gltf) => {
            scene.add(gltf.scene.children[0])
        });

        const renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true, antialias: true });
        renderer.setSize(sizes.width, sizes.height);

        function render(){
            renderer.render(scene, camera);
        }

        function update(){

        }

        const gameLoop = new GameLoop(update, render)
    },
}
</script>

<template>
    <div class="wrapper">
        <canvas class="canvas"></canvas>
    </div>
</template>

<style scoped>
.wrapper{
    display: flex;
    justify-content: center;
}
.canvas {
    width: 500px;
    height: 500px;
}
</style>
