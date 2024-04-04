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
      <edit-lines :initial-settings="bingoData.theme.line"></edit-lines>

      <edit-stamps :initial-settings="bingoData.theme.stamp" />
    </q-scroll-area>
  </q-drawer>
</template>

<script setup>
import { ref, watch } from "vue";
import EditFont from "./EditComponents/EditFont.vue";
import EditLines from "./EditComponents/EditLines.vue";
import EditStamps from "./EditComponents/EditStamps.vue";

const props = defineProps({
  isVisible: {
    type: Boolean,
    default: () => true,
  },
  bingoData: {
    type: Object,
  },
});

const emit = defineEmits(["update:isVisible", "update:bingoData"]);

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
