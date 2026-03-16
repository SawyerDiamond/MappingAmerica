<template>
    <div class="flex w-screen h-screen bg-[var(--primary-bg)]">
        <aside class="sidebar glass absolute top-4 left-4 bottom-4 w-[300px] flex flex-col p-4 overflow-y-auto z-[100] rounded-[20px] transition-transform duration-300">
            <div class="mb-4 pb-3 border-b border-[var(--glass-border)]">
                <div class="flex items-center justify-center gap-2 mt-2 mb-2">
                    <div class="css-flag" aria-hidden="true">
                        <div class="flag-canton"></div>
                    </div>
                    <h2 class="font-display text-[0.9rem] font-bold tracking-[0.03em] text-[var(--text-primary)] m-0">Mapping America</h2>
                </div>
            </div>
            <div class="flex flex-col gap-3">
                <div
                    v-for="inset in insets"
                    :key="inset.label"
                    class="w-full cursor-pointer rounded-[12px] overflow-hidden transition-all duration-200 border-2 border-transparent hover:scale-[1.02] hover:border-[var(--accent-color)] first:h-[160px] h-[140px]"
                    @click="jumpTo(inset)"
                >
                    <MapComponent
                        :center="inset.center"
                        :zoom="inset.zoom"
                        :isInset="true"
                        :label="inset.label"
                        :markers="[]"
                        @marker-click="handleMarkerClick"
                    />
                </div>
            </div>
        </aside>

        <main class="flex-1 relative">
            <MapComponent
                ref="mapRef"
                :zoom="4"
                :center="[-98.5795, 39.8283]"
                @marker-click="handleMarkerClick"
            />
            <ZoomControls
                @zoom-in="mapRef?.zoomIn()"
                @zoom-out="mapRef?.zoomOut()"
                @add-click="showAddModal = true"
                @home-click="showHome = true"
                @refresh-click="() => {}"
            />
            <LocationDetail
                :location="selectedLocation"
                @close="selectedLocation = null"
            />
        </main>

        <HomeScreen :show="showHome" @dismiss="showHome = false" />
    </div>
</template>

<script setup>
import { ref } from "vue";
import MapComponent from "./components/MapComponent.vue";
import ZoomControls from "./components/ZoomControls.vue";
import LocationDetail from "./components/LocationDetail.vue";
import HomeScreen from "./components/HomeScreen.vue";

const mapRef = ref(null);
const selectedLocation = ref(null);
const showAddModal = ref(false);
const showHome = ref(true);

const insets = [
    { label: "Alaska", center: [-152.479, 64.2], zoom: 2 },
    { label: "Hawaii", center: [-157.858, 21.306], zoom: 5 },
    { label: "Puerto Rico/USVI", center: [-66.1, 18.2], zoom: 6 },
    { label: "Guam/Northern Mariana", center: [144.7, 13.5], zoom: 7 },
    { label: "American Samoa", center: [-170.7, -14.3], zoom: 8 },
];

const handleMarkerClick = (location) => {
    selectedLocation.value = location;
};

const jumpTo = (target) => {
    if (mapRef.value) {
        const coords = target.coords || target.center;
        const zoom = target.zoom ? target.zoom + 2 : 8;
        mapRef.value.flyTo(coords, zoom);
    }
};
</script>

<style>
@import "./assets/main.css";

.css-flag {
    width: 28px;
    height: 19px;
    border-radius: 2px;
    background: repeating-linear-gradient(
        to bottom,
        #B22234 0px, #B22234 1.46px,
        #fff 1.46px, #fff 2.92px
    );
    position: relative;
    overflow: hidden;
    flex-shrink: 0;
}
.flag-canton {
    position: absolute;
    top: 0; left: 0;
    width: 42%; height: 53%;
    background: #3C3B6E;
}
</style>
