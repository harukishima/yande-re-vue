<script setup lang="ts">
interface ImagePostProps {
  file_url: string;
  tags: string;
  width: number;
  height: number;
  image_url: string;
}
const props = defineProps<ImagePostProps>()
</script>

<template>
<div style="display: flex; justify-content: center">
  <a :href="props.file_url" target="_blank">
    <img :alt="props.tags" :src="props.image_url" :height="props.height" :width="props.width" loading="lazy" />
  </a>
</div>
</template>

