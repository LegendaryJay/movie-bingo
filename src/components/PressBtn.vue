<template>
  <q-btn
    :style="`--button-color: ${props.color};`"
    flat
    :class="{
      'active-button': props.modelValue,
      'inactive-button': !props.modelValue,
    }"
    :icon="props.icon"
    @click="update"
  />
</template>

<script setup>
import { defineProps, toRefs, defineEmits, computed } from "vue";

const props = defineProps({
  modelValue: Boolean, // Renamed from `value`
  color: {
    type: String,
    default: () => "primary",
  },
  icon: String,
});

const emit = defineEmits(["update:modelValue"]);

function update() {
  emit("update:modelValue", !props.modelValue); // Emitting `update:modelValue`
}
</script>
<style lang="scss">
.inactive-button {
  background: transparent; // Dynamically set background color
  color: grey;
}

.active-button {
  background: rgba($primary, 0.2); // Example inactive background color
  color: black; // Dynamically set text color for inactive state
}
</style>
