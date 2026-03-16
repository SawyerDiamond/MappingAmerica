<template>
    <Transition name="home-fade">
        <div v-if="show" class="fixed inset-0 z-[500] flex flex-col bg-[#0c1810] cursor-pointer font-sans" @click="$emit('dismiss')">
            <!-- Background -->
            <div class="absolute inset-0">
                <img src="/LandingPhoto.webp" alt="American Flags" class="w-full h-full object-cover [object-position:center_30%]" />
                <div class="absolute inset-0 bg-[rgba(12,24,16,0.55)]"></div>
            </div>

            <!-- Nav -->
            <div class="relative z-10 px-10 pt-8">
                <span class="text-white/90 text-[11px] font-medium tracking-[0.25em] uppercase">Mapping America</span>
            </div>

            <!-- Hero -->
            <div class="relative z-10 flex-1 flex flex-col justify-center px-10 pb-8 max-w-[55%]">
                <div class="flex items-center gap-3 mb-5">
                    <div class="h-px w-6 bg-[rgba(237,232,212,0.6)]"></div>
                    <span class="text-[rgba(237,232,212,0.75)] text-[10px] tracking-[0.3em] uppercase">Washington, D.C.</span>
                </div>
                <h1 class="font-display text-[clamp(2rem,4vw,4rem)] font-extrabold leading-[1.05] text-white mb-4">
                    Every corner<br />
                    <span class="text-[#EDE8D4]">tells a story.</span>
                </h1>
                <p class="text-[1rem] leading-[1.65] text-white/65 max-w-[460px] m-0">
                    Real memories from real people — pinned to the places that shaped them.
                    Explore the map and see what makes America home.
                </p>
            </div>

            <!-- Bottom bar CTA -->
            <div class="relative z-10 flex items-center justify-center px-8 pt-5 pb-8 gap-8">
                <div class="flex flex-col items-center gap-3">
                    <div class="text-[11px] tracking-[0.2em] uppercase text-white/35">Touch anywhere to begin</div>
                    <button
                        class="inline-flex items-center gap-[0.6rem] px-8 py-3 border-[1.5px] border-[rgba(237,232,212,0.5)] rounded-full bg-[rgba(237,232,212,0.1)] backdrop-blur-[12px] text-[#EDE8D4] font-sans text-[0.85rem] font-semibold tracking-[0.04em] cursor-pointer transition-[background,border-color,transform] duration-200 hover:bg-[rgba(237,232,212,0.18)] hover:border-[rgba(237,232,212,0.8)] hover:-translate-y-0.5 active:scale-[0.97]"
                        @click.stop="$emit('dismiss')"
                    >
                        <span>Explore the Map</span>
                        <svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                            <line x1="5" y1="12" x2="19" y2="12"></line>
                            <polyline points="12 5 19 12 12 19"></polyline>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
    </Transition>
</template>

<script setup>
defineProps({ show: Boolean });
defineEmits(["dismiss"]);
</script>

<style scoped>
.home-fade-enter-active { transition: opacity 0.4s ease; }
.home-fade-leave-active { transition: opacity 0.5s ease; }
.home-fade-enter-from,
.home-fade-leave-to { opacity: 0; }
</style>
