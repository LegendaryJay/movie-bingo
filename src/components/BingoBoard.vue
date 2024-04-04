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
          :cell-settings="cell"
          :marker-settings="stamp"
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
  },
  scale: {
    tyle: Number,
    default: () => 1,
  },
});

const scale = props.scale;
const { title, cell, line, stamp } = props.bingoData.theme;

const titleText = props.bingoData.content.title;
const movieTropes = props.bingoData.content.cell;

const titleStyles = computed(() => ({
  height: `${title.size * scale}px`,
  backgroundColor: title.backgroundColor,
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
  textAlign: "center",
  fontSize: `${title.textSize * scale}px`,
  fontFamily: title.font,
  color: title.textColor,
  boxSizing: "border-box",
  width: `100%`,
  margin: `0 0 calc(${line.size} * ${scale}) 0`,
}));

const containerStyles = computed(() => {
  const alphaHex = Math.floor(255 * line.alpha)
    .toString(16)
    .padStart(2, "0");

  return {
    display: "grid",
    gridTemplateColumns: "repeat(5, 1fr)",
    gap: `${line.size * scale}px`,
    backgroundColor: `${line.color + alphaHex}`,
    padding: `${line.size * scale}px`,
  };
});

const boardStyles = computed(() => ({}));

const cardStyles = computed(() => ({
  padding: `${line.size * scale}px`,
  backgroundColor: title.backgroundColor,
  padding: `0 ${30 * scale}px ${30 * scale}px ${30 * scale}px`,
}));
</script>

<!-- {
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
  }, -->
