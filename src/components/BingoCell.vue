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
  content: {
    type: String,
  },
  scale: {
    type: Number,
  },
});

const marked = ref(false);

const cellStyle = computed(() => ({
  width: `calc((${props.cellSettings.size} + ${props.cellSettings.lineWidth}) * ${props.scale})`,
  height: `calc((${props.cellSettings.size} + ${props.cellSettings.lineWidth}) * ${props.scale})`,
  backgroundColor: props.cellSettings.backgroundColor,
  color: props.cellSettings.textColor,
  fontSize: `calc(${props.cellSettings.textSize} * ${props.scale})`,
  fontFamily: props.cellSettings.textFont,
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
  boxSizing: "border-box",
  position: "relative",
}));

const randomRotation = ref(0);
const randomXOffset = ref(50);
const randomYOffset = ref(50);
const randomImageIndex = ref(0);
function generateRandoms() {
  randomRotation.value = Math.floor(Math.random() * 360);
  randomXOffset.value =
    50 + (Math.random() - 0.5) * 50 * props.cellSettings.markerOffset;
  randomYOffset.value =
    50 + (Math.random() - 0.5) * 50 * props.cellSettings.markerOffset;
  randomImageIndex.value = Math.floor(Math.random() * 6);
}

watch(marked, (newValue, oldValue) => {
  generateRandoms();
});

const imageName = computed(() => {
  return `svguse:dabs.svg#dab-${randomImageIndex.value}`;
});

const imageSize = computed(
  () => `calc(${props.cellSettings.size} * ${props.cellSettings.markerSize})`,
);

const imageOpacity = computed(() => props.cellSettings.markerAlpha ?? 1);
const imageStyle = computed(() => ({
  position: "absolute",
  width: `${imageSize.value}`,
  height: `${imageSize.value}`,
  top: `${randomXOffset.value}%`,
  left: `${randomYOffset.value}%`,
  transform: `translate(-50%, -50%) rotate(${randomRotation.value}deg)`,
  zIndex: 1, // Ensure it's on top
  opacity: imageOpacity.value,
  color: `${props.cellSettings.markerColor}`,
}));

function toggleMark() {
  marked.value = !marked.value;
}
</script>

<style>
/* Make sure .text-center or another container class has the correct positioning */
.cell-container {
  position: relative; /* This ensures that your absolute positioning works as expected */
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  cursor: pointer;
  z-index: 2; /* Make sure this is above everything else in the .cell-container */
}
</style>
