<template>
  <edit-card>
    <div class="row justify-between q-pa-sm">
      <q-btn
        flat
        dense
        :style="{ color: settings.color, fill: '#ff0000' }"
        icon="format_color_text"
      >
        <q-popup-proxy>
          <q-color v-model="settings.color"></q-color>
        </q-popup-proxy>
      </q-btn>
      <q-btn
        flat
        dense
        :style="{ color: settings.backgroundColor }"
        icon="format_color_fill"
      >
        <q-popup-proxy>
          <q-color v-model="settings.backgroundColor"></q-color>
        </q-popup-proxy>
      </q-btn>
      <PressBtn icon="format_bold" v-model="settings.bold"> </PressBtn>
      <PressBtn icon="format_italic" v-model="settings.italic"> </PressBtn>
      <PressBtn icon="format_underline" v-model="settings.underline">
      </PressBtn>
    </div>
    <div class="row q-pa-sm justify-between">
      <q-select
        class="col-8"
        filled
        dense
        label="Font"
        :options="fontOptions"
        v-model="settings.font"
        :style="{ fontFamily: settings.font }"
        ref="fontSelect"
      >
        <template v-slot:option="slotProps">
          <q-item
            clickable
            @click="selectFont(slotProps.opt.value)"
            :style="{ fontFamily: slotProps.opt.value }"
          >
            <q-item-section>
              {{ slotProps.opt.label }}
            </q-item-section>
          </q-item>
        </template>
      </q-select>
      <q-input
        dense
        class="col-3"
        type="number"
        label="Font Size"
        v-model="settings.textSize"
      />
    </div>
  </edit-card>
</template>

<script setup>
import { ref, watch } from "vue";

import PressBtn from "../PressBtn.vue";
import EditCard from "./EditCard.vue";
const fontSelect = ref(null);

const props = defineProps({
  initialSettings: {
    type: Object,
  },
});

const emit = defineEmits(["update:settings"]);
const settings = ref({ ...props.initialSettings });

const fontOptions = [
  { label: "Arial", value: "Arial" },
  { label: "Verdana", value: "Verdana" },
  { label: "Helvetica", value: "Helvetica" },
  { label: "Tahoma", value: "Tahoma" },
  { label: "Trebuchet MS", value: "Trebuchet MS" },
  { label: "Times New Roman", value: "Times New Roman" },
  { label: "Georgia", value: "Georgia" },
  { label: "Garamond", value: "Garamond" },
  { label: "Courier New", value: "Courier New" },
  { label: "Brush Script MT", value: "Brush Script MT" },
];

const selectFont = (font) => {
  settings.value.font = font;
  fontSelect.value.hidePopup();
};
</script>
