<script setup>
import "aframe";
import { onMounted,ref } from "vue";
const count = ref("");
const oxigen = ref(100)
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
        <a-scene >
            <a-assets>
            </a-assets>
            <a-camera>
                <a-cursor material="color:white"></a-cursor>
                <a-text :value="'Oxygen: ' + oxigen + '%'" scale="0.5 0.5" opacity="0.5" color="#3192d3" position="2 2 -3"></a-text>
                <a-text :value="'SpO2: ' + oxigen + '%'" scale="0.4 0.4" opacity="1" color="#3192d3" position="-0.5 -1.75 -3"></a-text>
                <a-image src="proyecto-vr/visor.png" alpha-test position="0 0 -0.6" width="2"></a-image>
            </a-camera>
            <a-image width="2.5" src="proyecto-vr/button.png" position="0 1.5 -3"></a-image>
                <a-text :value="count" scale="0.3 0.3" opacity="0.5" color="#3192d3" position="-0.9 2 -3"></a-text>
                <a-sky color="#040D19"></a-sky>
        </a-scene>
    </main>
</template>

<style scoped>
</style>
