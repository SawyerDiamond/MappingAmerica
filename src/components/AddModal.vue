<template>
    <Transition name="fade">
        <div v-if="show" class="modal-overlay fixed inset-0 bg-black/70 backdrop-blur-md flex items-center justify-center z-1000 p-[2vw] font-sans" @click.self="$emit('close')">
            <div
                class="modal-content w-full max-w-[30vw] rounded-[1.5vw] p-[2.5vw] relative bg-[rgba(12,24,16,0.92)] backdrop-blur-[32px] backdrop-saturate-160 border border-white/9 shadow-[0_8px_60px_rgba(0,0,0,0.65),inset_0_1px_0_rgba(255,255,255,0.07)]"
                role="dialog"
                aria-modal="true"
                aria-labelledby="modal-title"
            >
                <!-- Close button -->
                <button
                    class="p-0 absolute top-[1.2vw] right-[1.2vw] w-[2.2vw] h-[2.2vw] rounded-full border border-white/12 bg-white/5 text-white/50 cursor-pointer flex items-center justify-center leading-none transition-colors duration-150 active:bg-white/15 active:text-white"
                    @click="$emit('close')"
                    aria-label="Close"
                >
                    <Icon icon="solar:close-circle-bold" class="size-[1vw]" />
                </button>

                <div class="text-center mb-[2vh]">
                    <div class="w-[3vw] h-[3vw] rounded-[0.8vw] bg-[rgba(212,168,83,0.1)] border border-[rgba(212,168,83,0.25)] text-(--accent-color) flex items-center justify-center mx-auto mb-[1.5vh]">
                        <Icon icon="solar:map-point-add-bold" class="size-[1.4vw]" />
                    </div>
                    <h2 id="modal-title" class="font-display text-[1.6vw] font-semibold text-white tracking-[-0.02em] mb-[0.5vh]">Share Your Story</h2>
                    <p class="text-[0.9vw] text-white/45 m-0">What makes America home to you?</p>
                </div>

                <!-- QR code placeholder -->
                <div class="rounded-[1vw] border-2 border-dashed border-white/10 bg-[rgba(22,34,19,0.6)] aspect-square w-[18vw] mx-auto flex items-center justify-center p-[1.5vw] transition-[border-color,background] duration-200 cursor-pointer active:border-[rgba(212,168,83,0.35)] active:bg-[rgba(22,34,19,0.8)]">
                    <div class="flex flex-col items-center gap-[1vh] text-white/22 text-[0.8vw] tracking-[0.03em]">
                        <svg xmlns="http://www.w3.org/2000/svg" class="size-[1.8vw]" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round">
                            <rect x="3" y="3" width="5" height="5" rx="1" ry="1"></rect>
                            <rect x="16" y="3" width="5" height="5" rx="1" ry="1"></rect>
                            <rect x="3" y="16" width="5" height="5" rx="1" ry="1"></rect>
                            <path d="M21 16v5"></path>
                            <path d="M16 21h5"></path>
                            <path d="M16 16h5"></path>
                            <path d="M21 8h-5V3"></path>
                            <path d="M3 8h5V3"></path>
                            <path d="M3 16h5v5"></path>
                            <path d="M12 8v8"></path>
                            <path d="M8 12h8"></path>
                        </svg>
                        <span>QR code goes here</span>
                    </div>
                </div>
            </div>
        </div>
    </Transition>
</template>

<script setup>
import { Icon } from "@iconify/vue";
defineProps({ show: Boolean });
defineEmits(["close"]);
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.28s ease;
}
.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
.fade-enter-active .modal-content {
    animation: modal-in 0.32s cubic-bezier(0.34, 1.56, 0.64, 1);
}
@keyframes modal-in {
    from { transform: scale(0.93) translateY(8px); opacity: 0; }
    to   { transform: scale(1) translateY(0); opacity: 1; }
}
</style>
