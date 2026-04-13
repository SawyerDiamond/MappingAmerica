<template>
    <div class="flex w-screen h-screen bg-(--primary-bg)">
        <aside class="sidebar glass absolute top-[1.5vh] left-[1vw] bottom-[1.5vh] w-[20vw] flex flex-col pt-[1.2vw] px-[1.2vw] pb-[0.75vw] overflow-y-auto z-100 rounded-[1.2vw] transition-transform duration-300">
            <div class="mb-[1vh]">
                <div class="flex items-center justify-center gap-[0.6vw] mt-[0.8vh] mb-[0.8vh]">
                    <div class="css-flag" aria-hidden="true">
                        <div class="flag-canton"></div>
                    </div>
                    <h2 class="font-display text-[0.9vw] font-bold tracking-[0.03em] text-(--text-primary) m-0">Mapping America</h2>
                </div>
            </div>
            <div class="flex flex-col justify-around flex-1">
                <div
                    v-for="inset in insets"
                    :key="inset.label"
                    class="w-full cursor-pointer rounded-[0.8vw] overflow-hidden transition-colors duration-200 border border-white/9 active:border-(--accent-color) first:h-[18vh] h-[15vh]"
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

        <main class="flex-1 relative" @mousemove="resetInactivity" @keydown="resetInactivity" @touchstart.passive="resetInactivity">
            <MapComponent
                :key="refreshKey"
                ref="mapRef"
                :zoom="4"
                :center="[-98.5795, 39.8283]"
                :markers="locations"
                @marker-click="handleMarkerClick"
            />
            <ZoomControls
                @zoom-in="mapRef?.zoomIn()"
                @zoom-out="mapRef?.zoomOut()"
                @add-click="showAddModal = true"
                @home-click="showHome = true"
                @refresh-click="refreshLocations"
            />
            <AddModal :show="showAddModal" @close="showAddModal = false" />
            <LocationDetail
                :location="selectedLocation"
                @close="selectedLocation = null"
            />
        </main>

        <HomeScreen :show="showHome" @dismiss="dismissHome" />
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import MapComponent from "./components/MapComponent.vue";
import ZoomControls from "./components/ZoomControls.vue";
import LocationDetail from "./components/LocationDetail.vue";
import AddModal from "./components/AddModal.vue";
import HomeScreen from "./components/HomeScreen.vue";

const mapRef = ref(null);
const selectedLocation = ref(null);
const showAddModal = ref(false);
const showHome = ref(true);
const locations = ref([]);
const refreshKey = ref(0);

const INACTIVITY_MS = 5 * 60 * 1000;
let inactivityTimer = null;

const API_BASE = import.meta.env.VITE_API_BASE_URL ?? "";

async function fetchLocations() {
    try {
        const res = await fetch(`${API_BASE}/locations`);
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        const data = await res.json();
        locations.value = data.locations ?? [];
    } catch (err) {
        console.error("Failed to load locations:", err);
    }
}

async function refreshLocations() {
    await fetchLocations();
    refreshKey.value++;
}

function resetInactivity() {
    clearTimeout(inactivityTimer);
    inactivityTimer = setTimeout(() => {
        showHome.value = true;
    }, INACTIVITY_MS);
}

function dismissHome() {
    showHome.value = false;
    resetInactivity();
}

onMounted(() => {
    fetchLocations();
    resetInactivity();
});

onUnmounted(() => {
    clearTimeout(inactivityTimer);
});

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
    width: 1.5vw;
    height: 1vw;
    border-radius: 0.1vw;
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
