<template>
    <div
        class="relative w-full h-full overflow-hidden"
        :class="isInset ? 'bg-(--secondary-bg)' : ''"
    >
        <div class="w-full h-full" ref="mapContainer"></div>
        <div
            v-if="label && isInset"
            class="absolute bottom-2.5 left-2.5 px-2.5 py-0.75 font-sans text-[0.62rem] font-semibold tracking-[0.08em] uppercase text-white/75 bg-[rgba(12,24,16,0.72)] backdrop-blur-[10px] border border-white/10 rounded-md pointer-events-none z-5 "
        >{{ label }}</div>
    </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref, watch } from "vue";
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";

const props = defineProps({
    markers: {
        type: Array,
        default: () => [],
    },
    zoom: {
        type: Number,
        default: 3,
    },
    center: {
        type: Array,
        default: () => [-98.5795, 39.8283],
    },
    isInset: {
        type: Boolean,
        default: false,
    },
    label: {
        type: String,
        default: "",
    },
    bounds: {
        type: Array,
        default: null,
    },
});

const emit = defineEmits(["marker-click"]);
const mapContainer = ref(null);
const map = ref(null);
const mapReady = ref(false);
const markerInstances = [];

onMounted(() => {
    mapboxgl.accessToken = import.meta.env.VITE_MAPBOX_PUBLIC;

    map.value = new mapboxgl.Map({
        container: mapContainer.value,
        style: "mapbox://styles/sdiamond05/cmmsq5stn002h01s3bm27dm95",
        center: props.center,
        zoom: props.zoom,
        projection: "globe",
        attributionControl: false,
        interactive: !props.isInset,
    });

    if (props.bounds) {
        map.value.fitBounds(props.bounds, { padding: 20, animate: false });
    }

    map.value.on("style.load", () => {
        try {
            map.value.setConfigProperty("basemap", "lightPreset", "night");
        } catch (e) {
            console.log("Light preset not available for this style");
        }
    });

    map.value.on("load", () => {
        mapReady.value = true;
        if (props.markers.length > 0) {
            addMarkers(props.markers);
        }
    });
});

onUnmounted(() => {
    markerInstances.forEach((m) => m.remove());
    markerInstances.length = 0;
});

const addMarkers = (markerList) => {
    markerList.forEach((markerData) => {
        const el = document.createElement("div");
        el.className = "map-pin";
        if (props.isInset) el.classList.add("mini");

        el.innerHTML = `
      <div class="pin-head">
        <img src="${markerData.image}" alt="${markerData.title}" />
      </div>
      <div class="pin-tail"></div>
    `;

        el.addEventListener("click", (e) => {
            e.stopPropagation();
            emit("marker-click", markerData);
            if (!props.isInset) {
                map.value.flyTo({
                    center: markerData.coords,
                    zoom: 15,
                    essential: true,
                });
            }
        });

        const instance = new mapboxgl.Marker({
            element: el,
            anchor: "bottom",
        })
            .setLngLat(markerData.coords)
            .addTo(map.value);

        markerInstances.push(instance);
    });
};

watch(
    () => props.zoom,
    (newZoom) => {
        if (map.value && !props.isInset) {
            map.value.setZoom(newZoom);
        }
    },
);

watch(
    () => props.markers,
    (newMarkers) => {
        if (!mapReady.value || !newMarkers.length) return;
        markerInstances.forEach((m) => m.remove());
        markerInstances.length = 0;
        addMarkers(newMarkers);
    },
);

defineExpose({
    zoomIn: () => map.value.zoomTo(map.value.getZoom() + 1),
    zoomOut: () => map.value.zoomTo(map.value.getZoom() - 1),
    flyTo: (coords, zoom = 8) => {
        map.value.flyTo({ center: coords, zoom, essential: true });
    },
});
</script>

<!-- Global styles targeting DOM elements injected by Mapbox GL — cannot use Tailwind scoped classes -->
<style>
.map-pin {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
}
.map-pin:active .pin-head {
    border-color: #d4a853;
    box-shadow: 0 0 0 3px rgba(212, 168, 83, 0.25), 0 6px 20px rgba(0, 0, 0, 0.5);
}

.pin-head {
    width: clamp(32px, 2.8vw, 56px);
    height: clamp(32px, 2.8vw, 56px);
    border-radius: 50%;
    overflow: hidden;
    border: 2.5px solid rgba(237, 232, 212, 0.75);
    box-shadow: 0 0 0 1.5px rgba(0, 0, 0, 0.35), 0 4px 14px rgba(0, 0, 0, 0.45);
    background: #162213;
    transition: border-color 0.15s ease, box-shadow 0.15s ease;
}
.pin-head img { width: 100%; height: 100%; object-fit: cover; display: block; border-radius: 50%; }

.pin-tail {
    width: 2px;
    height: clamp(8px, 0.7vw, 14px);
    background: linear-gradient(to bottom, rgba(255, 255, 255, 0.7), transparent);
    border-radius: 0 0 2px 2px;
    margin-top: -1px;
}

.map-pin.mini .pin-head {
    width: clamp(18px, 1.8vw, 34px);
    height: clamp(18px, 1.8vw, 34px);
    border-width: 2px;
}
.map-pin.mini .pin-tail { height: clamp(5px, 0.5vw, 10px); }
</style>
