<script setup lang="ts">
import { ref, computed } from "vue";
import Gallery from "vue-gallery";
import { ImageItem } from "./ImageItem";

let images = ref<ImageItem[]>([
  {
    id: "ghibli-001",
    title: "Floating Castle",
    description: "A serene castle drifting above a misty valley.",
    url: "https://media.discordapp.net/attachments/993935904093782149/1357418671089389688/raw.png?ex=67f2c526&is=67f173a6&hm=96cef492a8cc66c29fe1d3684e3824a6f1cf355f5b807f21aeff46edaa9a016f&=&format=webp&quality=lossless&width=873&height=873",
    createdAt: "2025-04-04T10:00:00Z",
    tags: ["castle", "sky", "dreamy"],
    likes: 32,
    views: 104,
  },
  {
    id: "ghibli-002",
    title: "Floating Castle",
    description: "A serene castle drifting above a misty valley.",
    url: "https://media.discordapp.net/attachments/993935904093782149/1357524862964600852/file_00000000aec851f7bb27f655eaafab9c_conversation_id67ed9816-4e2c-800e-96e4-0e7d5a0faf59message_id26af8803-1133-4198-8de4-1aec28d04749.png?ex=67f27f4c&is=67f12dcc&hm=ac2884ae8de137c339941bc20a38f155dbc25fff1781e45b14b5c92668873697&=&format=webp&quality=lossless&width=385&height=385",
    createdAt: "2025-04-04T10:00:00Z",
    tags: ["castle", "sky", "dreamy"],
    likes: 32,
    views: 104,
  },
]);

// Function to generate multiple copies of the existing images
function generateManyImages(count: number) {
  const originalImages = [...images.value];
  
  for (let i = 1; i < count; i++) {
    originalImages.forEach(img => {
      images.value.push({
        ...img,
        id: `${img.id}-copy-${i}`, // Create unique ID for each copy
      });
    });
  }
}

// Generate 50 copies of each image (resulting in 100+ total images)
generateManyImages(50);


const index = ref<number | null>(null);
const imageUrls = computed(() => images.value.map((item) => item.url));

function addLike(i: number) {
  images.value[i].likes++;
}

function addView(i: number) {
  images.value[i].views++;
}

function handleImageClick(i: number) {
  index.value = i;
  addView(i);
}
</script>
<template>
  <gallery :images="imageUrls" :index="index" @close="index = null" />
  <div class="flex flex-wrap justify-center">
    <div
      v-for="(image, idx) in images"
      :key="image.id"
      class="image-container m-6 border border-gray-300"
    >
      <div
        class="image bg-cover bg-center cursor-pointer"
        :style="{ backgroundImage: 'url(' + image.url + ')' }"
        style="width: 300px; height: 200px"
        @click="handleImageClick(idx)"
      ></div>

      <div class="image-info">
        <p class="text-gray-500 text-xs">
          {{ new Date(image.createdAt).toLocaleDateString() }}
        </p>
        <p class="text-gray-500 text-xs">
          Tags:
          <span v-for="tag in image.tags" :key="tag">
            {{ tag }}
            <span v-if="tag !== image.tags[image.tags.length - 1]">, </span>
            <span v-if="tag === image.tags[image.tags.length - 1]">.</span>
          </span>
        </p>
        <h3 class="font-semibold">{{ image.title }}</h3>
        <p class="text-gray-600">{{ image.description }}</p>

        <!-- This container separates Like on the left and Views on the right -->
        <div class="ml-2 action-buttons flex justify-between p-2">
          <button
            @click.stop="addLike(idx)"
            class="cursor-pointer hover:text-red-500 transition duration-200 transform hover:scale-105"
          >
            ❤️ {{ image.likes }}
          </button>

          <div class="cursor-default">👁️ {{ image.views }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.image {
  transition: transform 0.3s ease;
}
.image:hover {
  transform: scale(1.05);
}
.image-info {
  text-align: center;
  margin-top: 0.5rem;
}

.image-container {
  transition: transform 0.3s ease;
}
.image-container:hover {
  transform: scale(1.05);
}
</style>
