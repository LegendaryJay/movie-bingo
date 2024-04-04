<template>
  <div class="text-center cell-container" :style="cellStyle">
    <div class="overlay" @click="toggleMark"></div>
    {{ content }}
    <q-icon
      v-if="marked"
      :name="imageName"
      :style="imageStyle"
      alt="Decorative"
    />
  </div>
</template>

<script setup>
import { computed, ref, watch } from "vue";

// Props
const props = defineProps({
  cellSettings: {
    type: Object,
  },
  markerSettings: {
    type: Object,
  },
  content: {
    type: String,
  },
  scale: {
    type: Number,
  },
});

const marked = ref(false);
const randomRotation = ref(0);
const randomXOffset = ref(50);
const randomYOffset = ref(50);
const randomImageIndex = ref(0);
function generateRandoms() {
  randomRotation.value = Math.floor(Math.random() * 360);
  randomXOffset.value = 2 * Math.random() - 1;
  randomYOffset.value = 2 * Math.random() - 1;

  randomImageIndex.value = Math.floor(Math.random() * 6);
}

const cellStyle = computed(() => ({
  width: `${props.cellSettings.size * props.scale}px`,
  height: `${props.cellSettings.size * props.scale}px`,
  backgroundColor: props.cellSettings.backgroundColor,
  color: props.cellSettings.color,
  fontSize: `${props.cellSettings.textSize * props.scale}px`,
  fontFamily: props.cellSettings.font,
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
  boxSizing: "border-box",
  position: "relative",
}));

watch(marked, (newValue, oldValue) => {
  generateRandoms();
});

const imageName = computed(() => {
  return `svguse:dabs.svg#dab-${randomImageIndex.value}`;
});

const imageOpacity = computed(() => props.cellSettings.markerAlpha ?? 1);
const imageStyle = computed(() => {
  const imageSize = props.cellSettings.size * props.markerSettings.size;
  const alphaHex = Math.floor(255 * props.markerSettings.alpha)
    .toString(16)
    .padStart(2, "0");
  const color = props.markerSettings.color + alphaHex;
  const imgPlayPercent = 1 - imageSize / props.cellSettings.size;
  const imagePlay = imgPlayPercent * 50 * props.markerSettings.randomOffset;
  const x = 50 + randomXOffset.value * imagePlay;

  const y = 50 + randomYOffset.value * imagePlay;

  return {
    position: "absolute",
    width: `${imageSize}px`,
    height: `${imageSize}px`,
    top: `${x}%`,
    left: `${y}%`,
    transform: `translate(-50%, -50%) rotate(${randomRotation.value}deg)`,
    zIndex: 1, // Ensure it's on top
    opacity: imageOpacity.value,
    color,
  };
});

function toggleMark() {
  marked.value = !marked.value;
}
</script>

<style>
.cell-container {
  position: relative;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  cursor: pointer;
  z-index: 2;
}
</style>
