<template>
  <theme-drawer v-model:isVisible="drawer" settings></theme-drawer>
  <q-page class="flex flex-center">
    <q-btn @click="toggleDrawer"></q-btn>

    <bingo-board />
  </q-page>
</template>

<script setup>
import BingoBoard from "src/components/BingoBoard.vue";
import ThemeDrawer from "src/components/ThemeDrawer.vue";
import { ref } from "vue";

const settings = ref({
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
});
const props = defineProps({});
const drawer = ref(false);

function toggleDrawer() {
  drawer.value = !drawer.value;
}
</script>
