<script setup>
import "aframe";
import "aframe-extras"
import { computed } from 'vue'
import { onMounted,reactive,ref } from "vue";
import { useGamepad } from '@vueuse/core'
const count = ref("");
const oxigen = ref(100)


const spiderPosition = reactive({
    x:-5,
    y:0,
    z:-3  
})




onMounted(()=>{
    setInterval(()=>{
        spiderPosition.z += 0.5
    },100)
})

const btnPosition = reactive({
    x:-10,
    y:-5,
    z:-20
})

function handleClick(){
    alert("clicked!")
}

onMounted(()=>{
    // reloj de visor
    setInterval(()=>{
        const date = new Date();
        oxigen.value = oxigen.value - 0.1
        count.value = `${date.getMinutes()}m : ${date.getSeconds()}sec`
    },500)

    AFRAME.registerComponent("alpha-test",{
        dependencies:["material"],
        init:function(){
            let material = this.el.getObject3D("mesh").material;
            material.alphaTest = 0.5;
        }
    })
})

</script>

<template>
    <main class="absolute h-full w-full">
        <a-scene xr-mode-ui="enabled: true">
            <a-assets>
            </a-assets>
            <a-camera gamepad-controls="enabled:true">
                <a-cursor material="color:trasparent"></a-cursor>
                <a-text :value="gamepad" scale="0.4 0.4" opacity="0.7" color="white" position="-1.1 1.50 -3"></a-text>
                <a-image ref="btn" src="/proyecto-vr/visor.png" alpha-test position="0 0 -0.6" width="2"></a-image>
                <a-gltf-model  src="/proyecto-vr/rifle/scene.gltf" position="5 -4 -10" rotation=" 0 90 0" scale="0.1 0.1 0.1"></a-gltf-model>
            </a-camera>
            <a-gltf-model  src="/proyecto-vr/forest/scene.gltf" position="0 -5 1" rotation=" 0 -10 0" scale="2 2 2"></a-gltf-model>
            <a-gltf-model animation-mixer @click="handleClick"  src="/proyecto-vr/spider/scene.gltf" :position="' ' + spiderPosition.x + ' ' + spiderPosition.y + ' ' + spiderPosition.z" rotation="0 0 0" scale="0.3 0.3 0.3"></a-gltf-model>
            <button></button>
            <a-image width="2.5" src="/proyecto-vr/button.png" :position="btnPosition.x + ' ' + btnPosition.y + ' ' + btnPosition.z"></a-image>
            <a-text :value="count" scale="0.3 0.3" opacity="0.5" color="#3192d3" position="-0.9 2 -3"></a-text>
            <a-sky color="#040D19"></a-sky>
            <a-entity oculus-go-controls></a-entity>
            <a-entity oculus-touch-controls="hand: left"></a-entity>
            <a-entity oculus-touch-controls="hand: right">
                <a-gltf-model  src="/proyecto-vr/rifle/scene.gltf" position="5 -4 -10" rotation=" 0 90 0" scale="0.1 0.1 0.1"></a-gltf-model>
                </a-entity>
        </a-scene>
    </main>
</template>

<style scoped>
</style>
