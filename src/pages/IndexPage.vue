<template>
  <q-page class="flex flex-center">
    <bingo-board />
  </q-page>
</template>

<script setup>
import BingoBoard from "src/components/BingoBoard.vue";

defineOptions({
  name: "IndexPage",
});
</script>
