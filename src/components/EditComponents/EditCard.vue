<template>
  <q-card flat class="edit-card q-pa-md q-mb-md">
    <div>
      {{ title }}
    </div>
    <div>
      <slot></slot>
    </div>
  </q-card>
</template>

<script setup>
const props = defineProps({
  title: {
    type: String,
    default: "Title",
  },
});
</script>
<style lang="scss" scoped>
.edit-card {
  background-color: #f0f0ff;
}
</style>
