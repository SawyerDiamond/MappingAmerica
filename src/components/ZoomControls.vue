<template>
    <div class="absolute bottom-[4vh] right-[2vw] flex flex-col items-center gap-[1vh] z-10">
        <!-- Add/share button -->
        <button
            class="p-0 border-0 w-[2.8vw] h-[2.8vw] flex items-center justify-center cursor-pointer rounded-[1vw] bg-(--accent-color) text-(--accent-fg) shadow-[0_0_0_1px_rgba(237,232,212,0.3),0_4px_16px_rgba(237,232,212,0.15),0_2px_4px_rgba(0,0,0,0.4)] transition-[background,box-shadow] duration-180ms active:bg-[#d4a853] active:shadow-[0_0_0_1px_rgba(212,168,83,0.5),0_4px_16px_rgba(212,168,83,0.2),0_2px_4px_rgba(0,0,0,0.4)]"
            aria-label="Add Place"
            @click="$emit('add-click')"
        >
            <Icon icon="solar:map-point-add-bold" class="size-[1.1vw]" />
        </button>

        <!-- Home + Refresh group -->
        <div class="flex flex-col rounded-[1vw] overflow-hidden bg-[rgba(12,24,16,0.82)] backdrop-blur-lg backdrop-saturate-180 border border-white/8 shadow-[0_2px_20px_rgba(0,0,0,0.5),inset_0_1px_0_rgba(255,255,255,0.06)]" role="group">
            <button
                class="p-0 bg-transparent border-0 text-(--accent-color) w-[2.8vw] h-[2.8vw] flex items-center justify-center cursor-pointer rounded-[1vw] transition-colors duration-150 active:bg-white/10"
                aria-label="Home"
                @click="$emit('home-click')"
            >
                <Icon icon="solar:home-2-bold" class="size-[1.1vw]" />
            </button>
            <div class="h-px mx-[0.6vw] bg-white/7"></div>
            <button
                class="p-0 bg-transparent border-0 text-(--accent-color) w-[2.8vw] h-[2.8vw] flex items-center justify-center cursor-pointer rounded-[1vw] transition-colors duration-150 active:bg-white/10"
                aria-label="Refresh"
                @click="$emit('refresh-click')"
            >
                <Icon icon="solar:refresh-circle-bold" class="size-[1.1vw]" />
            </button>
        </div>

        <!-- Zoom controls -->
        <div class="flex flex-col rounded-[1vw] overflow-hidden bg-[rgba(12,24,16,0.82)] backdrop-blur-lg backdrop-saturate-180 border border-white/8 shadow-[0_2px_20px_rgba(0,0,0,0.5),inset_0_1px_0_rgba(255,255,255,0.06)]" role="group" aria-label="Map zoom">
            <button
                class="p-0 bg-transparent border-0 text-(--accent-color) w-[2.8vw] h-[2.8vw] flex items-center justify-center cursor-pointer rounded-[1vw] transition-colors duration-150 active:bg-white/10"
                @click="$emit('zoom-in')"
                aria-label="Zoom In"
            >
                <Icon icon="solar:magnifer-zoom-in-bold" class="size-[1.1vw]" />
            </button>
            <div class="h-px mx-[0.6vw] bg-white/7"></div>
            <button
                class="p-0 bg-transparent border-0 text-(--accent-color) w-[2.8vw] h-[2.8vw] flex items-center justify-center cursor-pointer rounded-[1vw] transition-colors duration-150 active:bg-white/10"
                @click="$emit('zoom-out')"
                aria-label="Zoom Out"
            >
                <Icon icon="solar:magnifer-zoom-out-bold" class="size-[1.1vw]" />
            </button>
        </div>
    </div>
</template>

<script setup>
import { Icon } from "@iconify/vue";
defineEmits(["zoom-in", "zoom-out", "add-click", "home-click", "refresh-click"]);
</script>
