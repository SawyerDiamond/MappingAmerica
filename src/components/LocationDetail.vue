<template>
    <Transition name="slide-up">
        <div
            v-if="location"
            class="absolute bottom-[1.5vh] left-[22vw] w-[22vw] rounded-[1.2vw] overflow-hidden z-200 glass shadow-[0_4px_40px_rgba(0,0,0,0.6),inset_0_1px_0_rgba(255,255,255,0.06),0_0_0_1px_rgba(0,0,0,0.3)] font-sans"
            role="dialog"
            aria-modal="true"
            :aria-label="location.title"
        >
            <button
                class="p-0 absolute top-[1vw] right-[1vw] z-10 w-[1.8vw] h-[1.8vw] rounded-full border border-(--accent-color)/20 bg-black/45 backdrop-blur-8px text-(--accent-color) cursor-pointer flex items-center justify-center leading-none transition-colors duration-150 active:bg-white/15"
                @click="$emit('close')"
                aria-label="Close"
            >
                <Icon icon="solar:close-circle-bold" class="size-[0.9vw]" />
            </button>

            <div class="relative w-full h-[22vh]">
                <img :src="location.image" :alt="location.title" class="w-full h-full object-cover block" />
                <div class="absolute inset-0 bg-linear-to-b from-transparent from-30% to-[rgba(10,13,20,0.75)]"></div>
            </div>

            <div class="px-[1.5vw] pt-[1.2vw] pb-[1.5vw]">
                <div class="flex items-center gap-[0.4vw] mb-[0.6vw]">
                    <span class="w-[0.35vw] h-[0.35vw] rounded-full bg-(--accent-color) shadow-[0_0_6px_rgba(212,168,83,0.7)] shrink-0"></span>
                    <span class="text-[0.7vw] font-mono text-(--accent-color) tracking-[0.04em] opacity-90">
                        {{ location.coords[1].toFixed(4) }}° N &nbsp;·&nbsp; {{ location.coords[0].toFixed(4) }}° W
                    </span>
                </div>
                <h2 class="font-display font-semibold text-[1.2vw] text-white mb-[0.5vw] leading-tight tracking-[-0.01em]">{{ location.title }}</h2>
                <p class="text-[0.8vw] leading-[1.6] text-white/55 m-0">{{ location.description }}</p>
            </div>
        </div>
    </Transition>
</template>

<script setup>
import { Icon } from "@iconify/vue";
defineProps({
    location: {
        type: Object,
        default: null,
    },
});
defineEmits(["close"]);
</script>

<style scoped>
.slide-up-enter-active,
.slide-up-leave-active {
    transition: all 0.42s cubic-bezier(0.16, 1, 0.3, 1);
}
.slide-up-enter-from,
.slide-up-leave-to {
    transform: translateY(16px);
    opacity: 0;
}
</style>
