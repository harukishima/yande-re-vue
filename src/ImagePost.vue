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
  <div>
    <a :href="props.file_url" target="_blank">
      <img :alt="props.tags" :src="props.image_url" loading="lazy"/>
    </a>
  </div>
</template>

<style>
img {
  max-width: 90%;
  height: auto;
  margin-left: auto;
  margin-right: auto;
  display: flex;
  justify-content: center;
}
</style>
