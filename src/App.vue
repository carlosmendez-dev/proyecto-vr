<script setup>
import "aframe";
import { onMounted,reactive,ref } from "vue";
const count = ref("");
const oxigen = ref(100)


const btnPosition = reactive({
    x:0,
    y:1.5,
    z:-3
})

const btnDangerPosition = reactive({
    x:0,
    y:0.5,
    z:-3
})

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
                <a-cursor material="color:trasparent"></a-cursor>
                <a-text :value="'Oxygen: ' + oxigen + '%'" scale="0.4 0.4" opacity="0.7" color="white" position="-1.1 1.50 -3"></a-text>
                <a-image ref="btn" src="/proyecto-vr/visor.png" alpha-test position="0 0 -0.6" width="2"></a-image>
            </a-camera>
            <a-image width="2.5" src="/proyecto-vr/button.png" :position="btnPosition.x + ' ' + btnPosition.y + ' ' + btnPosition.z"></a-image>
                <a-text :value="count" scale="0.3 0.3" opacity="0.5" color="#3192d3" position="-0.9 2 -3"></a-text>
                <a-sky color="#040D19"></a-sky>
        </a-scene>
    </main>
</template>

<style scoped>
</style>
