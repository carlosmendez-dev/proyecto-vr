<script setup>
import "aframe";
</script>

<template>
    <main class="absolute h-full w-full">
        <a-scene >
            <a-camera>
                <a-cursor></a-cursor>
            </a-camera>
            <a-box position="0 1 -2" color="#77B6EA"></a-box>
        </a-scene>
    </main>
</template>

<style scoped>
</style>
