<template>
  <q-card class="rounded-borders" :style="cardStyles">
    <div class="board-container" :style="boardStyles">
      <div class="title-container" :style="titleStyles">
        {{ titleText }}
      </div>
      <div class="grid-container" :style="containerStyles">
        <bingo-cell
          v-for="(trope, index) in movieTropes"
          :key="index"
          :content="trope"
          :cell-settings="cellSettings"
          :scale="scale"
        />
      </div>
    </div>
  </q-card>
</template>

<script setup>
import BingoCell from "./BingoCell.vue";
import { computed } from "vue";

const props = defineProps({
  bingoData: {
    type: Object,
    default: () => ({
      distortion: {
        scale: 1,
      },
      theme: {
        global: {
          size: "150px",
          backgroundColor: "#2A2D34",
          lineWidth: "8px",
          lineColor: "trnsparent",
          textColor: "#E0FBFC",
          textFont: "'Segoe UI', Arial, sans-serif",
          textSize: "18px",
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
          markerAlpha: 0.6, //0-1
          markerColor: "teal",
          markerOffset: 0.6, //0-1
          markerSize: 0.7, //0-1
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

const scale = props.bingoData.distortion.scale;
const { global, title, cell } = props.bingoData.theme;

// Function to merge theme settings, with specific settings overriding global ones
function mergeThemeSettings(globalSettings, specificSettings) {
  return { ...globalSettings, ...specificSettings };
}

const titleSettings = mergeThemeSettings(global, title);
const cellSettings = mergeThemeSettings(global, cell);

const titleText = props.bingoData.content.title;
const movieTropes = props.bingoData.content.cell;

const titleStyles = computed(() => ({
  height: `calc(${titleSettings.size} * ${scale})`, // Using global.size for height as per the requirement
  backgroundColor: titleSettings.backgroundColor,
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
  textAlign: "center",
  fontSize: `calc(${titleSettings.textSize} * ${scale})`,
  fontFamily: titleSettings.textFont,
  color: titleSettings.textColor,
  boxSizing: "border-box",
  width: `100%`,
  margin: `0 0 calc(${titleSettings.lineWidth} * ${scale}) 0`,
}));

const containerStyles = computed(() => ({
  display: "grid",
  gridTemplateColumns: "repeat(5, 1fr)",
  gap: `calc(${cellSettings.lineWidth} * ${scale})`,
  backgroundColor: cellSettings.lineColor,
  padding: `calc(${titleSettings.lineWidth} * ${scale})`,
}));

const boardStyles = computed(() => ({}));

const cardStyles = computed(() => ({
  padding: `calc(${titleSettings.lineWidth} * ${scale})`,
  backgroundColor: titleSettings.backgroundColor,
  padding: `0 calc(30px * ${scale}) calc(30px * ${scale}) calc(30px * ${scale})`,
}));
</script>
