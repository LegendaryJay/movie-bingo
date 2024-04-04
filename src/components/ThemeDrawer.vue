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
      <edit-lines :initial-settings="bingoData.theme.lines"></edit-lines>

      <edit-stamps :initial-settings="bingoData.theme.stamps" />
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
          size: 8,
          color: "#FF0000",
        },
        title: {
          color: "#000000",
          backgroundColor: "#227C9D",
          bold: false,
          italic: false,
          underline: false,
          font: "Arial",
          textSize: 40,
        },
        cell: {
          size: 140,
          bold: false,
          italic: false,
          underline: false,
          backgroundColor: "#16213E",
          textSize: 16,
          color: "#E0FBFC",
          font: "Arial",
        },
        stamps: {
          alpha: 0.6,
          color: "#16213E",
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
