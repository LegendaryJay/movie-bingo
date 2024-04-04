<template>
  <edit-card title="Stamp">
    <q-btn
      dense
      flat
      icon="format_color_fill"
      class="full-width"
      :style="{ color: settings.color }"
    >
      <q-popup-proxy>
        <q-color v-model="settings.color" />
      </q-popup-proxy>
    </q-btn>
    <div class="row">
      <q-icon size="md" name="opacity" class="q-pr-md" />
      <q-slider
        class="col"
        label
        :label-value="`Opacity: ${(settings.alpha * 100).toFixed()}%`"
        v-model="settings.alpha"
        :step="0.025"
        :min="0"
        :max="1"
      ></q-slider>
    </div>
    <div class="row">
      <q-icon size="md" name="sym_s_width" class="q-pr-md" />
      <q-slider
        class="col"
        v-model="settings.size"
        label
        :label-value="`Size: ${(settings.size * 100).toFixed()}% of the cell`"
        :step="0.025"
        :min="0"
        :max="1"
      ></q-slider>
    </div>
    <div class="row">
      <q-icon size="md" name="casino" class="q-pr-md" />
      <q-slider
        class="col"
        label
        :label-value="`Randomness: ${(settings.randomOffset * 100).toFixed(1)}%`"
        v-model="settings.randomOffset"
        :step="0.025"
        :min="0"
        :max="1"
      ></q-slider>
    </div>
  </edit-card>
</template>

<script setup>
import { ref, watch } from "vue";
import EditCard from "./EditCard.vue";

const props = defineProps({
  initialSettings: {
    type: Object,
  },
});

const settings = ref(props.initialSettings);
const emit = defineEmits(["update:initialSettings"]);
watch(
  settings,
  (newValue) => {
    emit("update:initialSettings", newValue);
  },
  { deep: true },
);
</script>
