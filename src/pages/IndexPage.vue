<template>
  <theme-drawer v-model:isVisible="drawer"></theme-drawer>
  <q-page class="flex flex-center">
    <q-btn @click="toggleDrawer"></q-btn>

    <bingo-board />
  </q-page>
</template>

<script setup>
import BingoBoard from "src/components/BingoBoard.vue";
import ThemeDrawer from "src/components/ThemeDrawer.vue";
import { ref } from "vue";

const drawer = ref(false);

function toggleDrawer() {
  drawer.value = !drawer.value;
}
defineOptions({
  name: "IndexPage",
});
</script>
