<template>
  <q-btn
    :style="`--button-color: ${props.color};`"
    flat
    dense
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
  emit("update:modelValue", !props.modelValue);
}
</script>
<style lang="scss">
.inactive-button {
  background: transparent;
  color: grey;
}

.active-button {
  background: rgba($primary, 0.2);
  color: black;
}
</style>
