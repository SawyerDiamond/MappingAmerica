<template>
    <Transition name="fade">
        <div v-if="show" class="modal-overlay fixed inset-0 bg-black/70 backdrop-blur-[6px] flex items-center justify-center z-[1000] p-4 font-sans" @click.self="$emit('close')">
            <div
                class="modal-content w-full max-w-[460px] rounded-[24px] p-[2.25rem] relative bg-[rgba(10,13,20,0.88)] backdrop-blur-[32px] backdrop-saturate-[160%] border border-white/[0.09] shadow-[0_8px_60px_rgba(0,0,0,0.65),inset_0_1px_0_rgba(255,255,255,0.07)]"
                role="dialog"
                aria-modal="true"
                aria-labelledby="modal-title"
            >
                <button
                    class="absolute top-[1.1rem] right-[1.1rem] w-[30px] h-[30px] rounded-full border border-white/[0.12] bg-white/5 text-white/50 cursor-pointer flex items-center justify-center transition-all duration-150 hover:bg-white/10 hover:text-white hover:scale-[1.08] hover:border-white/20 active:scale-[0.93]"
                    @click="$emit('close')"
                    aria-label="Close"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                        <line x1="18" y1="6" x2="6" y2="18"></line>
                        <line x1="6" y1="6" x2="18" y2="18"></line>
                    </svg>
                </button>

                <div class="text-center mb-[1.75rem]">
                    <div class="w-12 h-12 rounded-[14px] bg-[rgba(212,168,83,0.1)] border border-[rgba(212,168,83,0.25)] text-[var(--accent-color)] flex items-center justify-center mx-auto mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
                            <circle cx="12" cy="10" r="3"></circle>
                        </svg>
                    </div>
                    <h2 id="modal-title" class="font-display text-[1.6rem] font-semibold text-white tracking-[-0.02em] mb-[0.4rem]">Share Your Story</h2>
                    <p class="text-[0.9rem] text-white/45 m-0">What makes America home to you?</p>
                </div>

                <div class="rounded-[16px] border-[1.5px] border-dashed border-white/10 bg-white/[0.02] aspect-square w-[240px] mx-auto mb-[1.75rem] flex items-center justify-center p-4 transition-[border-color,background] duration-200 cursor-pointer hover:border-[rgba(212,168,83,0.35)] hover:bg-[rgba(212,168,83,0.03)]">
                    <div class="flex flex-col items-center gap-3 text-white/[0.22] text-[0.8rem] tracking-[0.03em] hover:text-[rgba(212,168,83,0.5)]">
                        <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round">
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

                <div class="flex justify-end">
                    <button
                        class="inline-flex items-center gap-[0.45rem] px-6 py-[0.7rem] border-0 rounded-[12px] bg-[var(--accent-color)] text-[#0d0f14] font-sans text-[0.85rem] font-semibold tracking-[0.02em] cursor-pointer shadow-[0_0_0_1px_rgba(212,168,83,0.4),0_4px_14px_rgba(212,168,83,0.22)] transition-[transform,box-shadow,background] duration-[180ms] hover:-translate-y-0.5 hover:bg-[#e2b96a] hover:shadow-[0_0_0_1px_rgba(212,168,83,0.55),0_8px_20px_rgba(212,168,83,0.3)] active:scale-[0.97] active:duration-[80ms]"
                        @click="$emit('close')"
                    >
                        <span>Got it</span>
                        <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                            <polyline points="9 18 15 12 9 6"></polyline>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
    </Transition>
</template>

<script setup>
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
