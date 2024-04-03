<template>
  <q-drawer
    side="right"
    :model-value="isVisible"
    @update:model-value="handleUpdate"
    show-if-above
    :width="300"
    :breakpoint="500"
  >
    <q-scroll-area class="fit q-pa-md">
      <edit-font
        title="Card and Title"
        :initial-settings="bingoData.theme.title"
      ></edit-font>
      <edit-font
        title="Boxes"
        :initial-settings="bingoData.theme.cell"
      ></edit-font>
      <edit-lines></edit-lines>
      <edit-card title="Lines">
        <q-btn dense flat icon="format_color_fill" class="full-width">
          <q-popup-proxy>
            <q-color v-model="settings.theme.lines.color" />
          </q-popup-proxy>
        </q-btn>
        <div class="row">
          <q-icon size="md" name="opacity" class="q-pr-md" />
          <q-slider class="col" v-model="settings.theme.lines.alpha"></q-slider>
        </div>
        <div class="row">
          <q-icon size="md" name="sym_s_width" class="q-pr-md" />
          <q-slider class="col" v-model="settings.theme.lines.size"></q-slider>
        </div>
      </edit-card>
      <edit-stamps />
      <edit-card title="Stamp">
        <q-btn dense flat icon="format_color_fill" class="full-width">
          <q-popup-proxy>
            <q-color v-model="settings.theme.stamp.color" />
          </q-popup-proxy>
        </q-btn>
        <div class="row">
          <q-icon size="md" name="opacity" class="q-pr-md" />
          <q-slider class="col" v-model="settings.theme.stamp.alpha"></q-slider>
        </div>
        <div class="row">
          <q-icon size="md" name="sym_s_width" class="q-pr-md" />
          <q-slider class="col" v-model="settings.theme.stamp.size"></q-slider>
        </div>
        <div class="row">
          <q-icon size="md" name="casino" class="q-pr-md" />
          <q-slider
            class="col"
            v-model="settings.theme.stamp.randomOffset"
          ></q-slider>
        </div>
      </edit-card>
    </q-scroll-area>
  </q-drawer>
</template>

<script setup>
import { ref, watch } from "vue";
import EditFont from "./EditComponents/EditFont.vue";
import EditCard from "./EditComponents/EditCard.vue";
import EditLines from "./EditComponents/EditLines.vue";
import EditStamps from "./EditComponents/EditStamps.vue";

const props = defineProps({
  isVisible: {
    type: Boolean,
    default: () => true,
  },
  bingoData: {
    type: Object,
    default: () => ({
      distortion: {
        scale: 1,
      },
      theme: {
        lines: {
          alpha: 0.6,
          size: "8px",
          color: "red",
        },
        title: {
          textSize: "40px",
          backgroundColor: "#227C9D",
        },
        cell: {
          size: "140px",
          backgroundColor: "#16213E",
          textSize: "16px",
          textColor: "#E0FBFC",
        },
        stamp: {
          alpha: 0.6,
          color: "teal",
          randomOffset: 0.6,
          size: 0.65,
        },
      },
      content: {
        title: "Your Movie Tropes Bingo",
        cell: [
          "Chosen One",
          "Love Triangle",
          "The Mentor Dies",
          "Secret Backstory",
          "Evil Villain Monologue",
          "The Big Twist",
          "Unlikely Hero",
          "Time Loop",
          "The MacGuffin",
          "Red Herring",
          "All Just a Dream",
          "Deadly Premonition",
          "Betrayal by Ally",
          "Final Showdown",
          "Race Against Time",
          "Hidden Powers",
          "Doppelganger",
          "Forbidden Love",
          "The Heist",
          "Undercover Misunderstanding",
          "Revenge Plot",
          "Coming of Age",
          "Tragic Backstory",
          "Heroic Sacrifice",
          "Villain's Redemption",
        ],
      },
    }),
  },
});

const emit = defineEmits(["update:isVisible"]);

const handleUpdate = (newValue) => {
  emit("update:isVisible", newValue);
};

const settings = ref(props.bingoData);

watch(
  settings,
  (newValue) => {
    emit("update:bingoData", newValue);
  },
  { deep: true },
);
</script>
