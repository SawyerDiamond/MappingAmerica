<template>
    <div class="flex w-screen h-screen bg-[var(--primary-bg)]">
        <main class="flex-1 relative">
            <MapComponent :zoom="4" :center="[-98.5795, 39.8283]" />
        </main>
    </div>
</template>

<script setup>
import MapComponent from "./components/MapComponent.vue";
</script>

<style>
@import "./assets/main.css";
</style>
