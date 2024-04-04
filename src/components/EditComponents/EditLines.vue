<template>
  <edit-card title="Lines">
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
        label
        :label-value="`Size: ${settings.size}px`"
        v-model="settings.size"
        :step="1"
        :min="0"
        :max="30"
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
