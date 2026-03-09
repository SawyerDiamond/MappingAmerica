<template>
    <Transition name="slide-up">
        <div
            v-if="location"
            class="absolute bottom-8 left-8 w-[calc(100%-4rem)] max-w-[360px] md:left-[330px] md:bottom-6 md:w-[340px] rounded-[20px] overflow-hidden z-[200] bg-[rgba(10,13,20,0.82)] backdrop-blur-[24px] backdrop-saturate-[160%] border border-white/[0.09] shadow-[0_4px_40px_rgba(0,0,0,0.6),inset_0_1px_0_rgba(255,255,255,0.06),0_0_0_1px_rgba(0,0,0,0.3)] font-sans"
            role="dialog"
            aria-modal="true"
            :aria-label="location.title"
        >
            <button
                class="absolute top-[0.85rem] right-[0.85rem] z-10 w-7 h-7 rounded-full border border-white/[0.15] bg-black/45 backdrop-blur-[8px] text-white/75 cursor-pointer flex items-center justify-center transition-[background,color,transform] duration-150 hover:bg-white/[0.12] hover:text-white hover:scale-[1.08] active:scale-[0.93]"
                @click="$emit('close')"
                aria-label="Close"
            >
                <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="18" y1="6" x2="6" y2="18"></line>
                    <line x1="6" y1="6" x2="18" y2="18"></line>
                </svg>
            </button>

            <div class="relative w-full h-[175px]">
                <img :src="location.image" :alt="location.title" class="w-full h-full object-cover block" />
                <div class="absolute inset-0 bg-gradient-to-b from-transparent from-[30%] to-[rgba(10,13,20,0.75)]"></div>
            </div>

            <div class="px-[1.35rem] pt-[1.1rem] pb-[1.35rem]">
                <div class="flex items-center gap-[0.45rem] mb-[0.55rem]">
                    <span class="w-1.5 h-1.5 rounded-full bg-[var(--accent-color)] shadow-[0_0_6px_rgba(212,168,83,0.7)] shrink-0"></span>
                    <span class="text-[0.7rem] font-mono text-[var(--accent-color)] tracking-[0.04em] opacity-90">
                        {{ location.coords[1].toFixed(4) }}° N &nbsp;·&nbsp; {{ location.coords[0].toFixed(4) }}° W
                    </span>
                </div>
                <h2 class="font-display font-semibold text-[1.35rem] text-white mb-[0.55rem] leading-[1.25] tracking-[-0.01em]">{{ location.title }}</h2>
                <p class="text-[0.85rem] leading-[1.6] text-white/55 m-0">{{ location.description }}</p>
            </div>
        </div>
    </Transition>
</template>

<script setup>
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
