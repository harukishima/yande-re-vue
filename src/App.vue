<script setup lang="ts">
import axios from "axios";

interface Post {
  id: number
  tags: string
  created_at: number
  updated_at: number
  creator_id: number
  approver_id: any
  author: string
  change: number
  source: string
  score: number
  md5: string
  file_size: number
  file_ext: string
  file_url: string
  is_shown_in_index: boolean
  preview_url: string
  preview_width: number
  preview_height: number
  actual_preview_width: number
  actual_preview_height: number
  sample_url: string
  sample_width: number
  sample_height: number
  sample_file_size: number
  jpeg_url: string
  jpeg_width: number
  jpeg_height: number
  jpeg_file_size: number
  rating: string
  is_rating_locked: boolean
  has_children: boolean
  parent_id: any
  status: string
  is_pending: boolean
  width: number
  height: number
  is_held: boolean
  frames_pending_string: string
  frames_pending: any[]
  frames_string: string
  frames: any[]
  is_note_locked: boolean
  last_noted_at: number
  last_commented_at: number
}

import {onMounted, ref} from "vue";
import ImagePost from "@/ImagePost.vue";

const posts = ref<Post[]>([]);
const tags = ref<string>('');
const page = ref<number>(1);
const fetchPosts = async () => {
  window.scrollTo(0, 0);
  posts.value = [];
  const {data} = await axios.get<Post[]>(`https://yande.re/post.json`, {
    params: {
      tags: tags.value,
      page: page.value
    }
  });
  posts.value = data;
}
onMounted(() => {
  fetchPosts();
});
const nextPage = () => {
  page.value++;
  fetchPosts();
}
const prevPage = () => {
  if (page.value > 1) {
    page.value--;
    fetchPosts();
  }
}

const onSubmit = async () => {
  page.value = 1;
  await fetchPosts();
}
</script>

<template>
  <div style="position: fixed; z-index: 10">
    <form @submit.prevent="onSubmit">
      <input v-model="tags" type="text" placeholder="Tags"/>
      <button>Search</button>
    </form>

    <div style="position: fixed; z-index: 9; right: 20px; bottom: 20px">
      <button @click="prevPage">Previous</button>
      <span>{{ page }}</span>
      <button @click="nextPage">Next</button>
    </div>
  </div>
  <ImagePost v-for="post in posts" :key="post.id" :file_url="post.file_url" :tags="post.tags"
             :width="post.sample_width" :height="post.sample_height" :image_url="post.jpeg_url"/>
</template>