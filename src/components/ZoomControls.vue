<template>
    <div class="absolute bottom-8 right-8 flex flex-col items-center gap-[0.6rem] z-10">
        <!-- Add button -->
        <button
            class="border-0 w-[42px] h-[42px] flex items-center justify-center cursor-pointer rounded-[14px] bg-[var(--accent-color)] text-[var(--accent-fg)] shadow-[0_0_0_1px_rgba(237,232,212,0.3),0_4px_16px_rgba(237,232,212,0.15),0_2px_4px_rgba(0,0,0,0.4)] transition-[transform,box-shadow,background] duration-[180ms] ease-[cubic-bezier(0.34,1.56,0.64,1)] hover:-translate-y-0.5 hover:scale-[1.04] hover:bg-[#f5f0e0] hover:shadow-[0_0_0_1px_rgba(237,232,212,0.5),0_8px_24px_rgba(237,232,212,0.2),0_2px_6px_rgba(0,0,0,0.4)] active:scale-[0.94] active:duration-[80ms]"
            aria-label="Add Place"
            @click="$emit('add-click')"
        >
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                <line x1="12" y1="5" x2="12" y2="19"></line>
                <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
        </button>

        <!-- Home + Refresh group -->
        <div class="flex flex-col rounded-[14px] overflow-hidden bg-[rgba(14,17,24,0.72)] backdrop-blur-[16px] backdrop-saturate-[180%] border border-white/[0.08] shadow-[0_2px_20px_rgba(0,0,0,0.5),inset_0_1px_0_rgba(255,255,255,0.06)]" role="group">
            <button
                class="bg-transparent border-0 text-white/70 w-[42px] h-[42px] flex items-center justify-center cursor-pointer transition-all duration-150 hover:text-[var(--accent-color)] hover:bg-white/5 active:scale-[0.88] active:bg-[rgba(237,232,212,0.08)]"
                aria-label="Home"
                @click="$emit('home-click')"
            >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                    <polyline points="9 22 9 12 15 12 15 22"></polyline>
                </svg>
            </button>
            <div class="h-px mx-2.5 bg-white/[0.07]"></div>
            <button
                class="bg-transparent border-0 text-white/70 w-[42px] h-[42px] flex items-center justify-center cursor-pointer transition-all duration-150 hover:text-[var(--accent-color)] hover:bg-white/5 active:scale-[0.88] active:bg-[rgba(237,232,212,0.08)]"
                aria-label="Refresh"
                @click="$emit('refresh-click')"
            >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <polyline points="23 4 23 10 17 10"></polyline>
                    <path d="M20.49 15a9 9 0 1 1-2.12-9.36L23 10"></path>
                </svg>
            </button>
        </div>

        <!-- Zoom controls -->
        <div class="flex flex-col rounded-[14px] overflow-hidden bg-[rgba(14,17,24,0.72)] backdrop-blur-[16px] backdrop-saturate-[180%] border border-white/[0.08] shadow-[0_2px_20px_rgba(0,0,0,0.5),inset_0_1px_0_rgba(255,255,255,0.06)]" role="group" aria-label="Map zoom">
            <button
                class="bg-transparent border-0 text-white/70 w-[42px] h-[42px] flex items-center justify-center cursor-pointer transition-all duration-150 hover:text-[var(--accent-color)] hover:bg-white/5 active:scale-[0.88] active:bg-[rgba(237,232,212,0.08)]"
                @click="$emit('zoom-in')"
                aria-label="Zoom In"
            >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="12" y1="5" x2="12" y2="19"></line>
                    <line x1="5" y1="12" x2="19" y2="12"></line>
                </svg>
            </button>
            <div class="h-px mx-2.5 bg-white/[0.07]"></div>
            <button
                class="bg-transparent border-0 text-white/70 w-[42px] h-[42px] flex items-center justify-center cursor-pointer transition-all duration-150 hover:text-[var(--accent-color)] hover:bg-white/5 active:scale-[0.88] active:bg-[rgba(237,232,212,0.08)]"
                @click="$emit('zoom-out')"
                aria-label="Zoom Out"
            >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="5" y1="12" x2="19" y2="12"></line>
                </svg>
            </button>
        </div>
    </div>
</template>

<script setup>
defineEmits(["zoom-in", "zoom-out", "add-click", "home-click", "refresh-click"]);
</script>
