<script setup lang="ts">

import { computed, ref } from 'vue';
import Fuse from 'fuse.js'

const searchItems = [
  {
    "name": "りんご",
    "description": "赤や緑、黄色などの色をしている果物です。お菓子や飲み物の材料にもなります。"
  },
  {
    "name": "ばなな",
    "description": "黄色い曲がった形の熱帯果物です。ビタミンCが豊富で栄養価が高い果物です。"
  },
  {
    "name": "みかん",
    "description": "橙色で香り高い柑橘類の果物です。缶詰やジュースにも加工されています。"
  },
  {
    "name": "ぶどう",
    "description": "小さな実がたくさんついた果物です。ワインの原料にもなります。"
  },
  {
    "name": "ストロベリー",
    "description": "赤い心形の果実で香りが良く、ケーキや飲み物に使われることが多い果物です。"
  },
  {
    "name": "オレンジ",
    "description": "橙色で香り高い柑橘類の果物です。ジュースやお菓子の材料によく使われます。"
  },
  {
    "name": "キウイフルーツ",
    "description": "中は緑色で、毛が生えた不思議な形の果物です。ビタミンCが豊富で栄養価が高い果物です。"
  },
  {
    "name": "パイナップル",
    "description": "鱗片状の表面が特徴的な熱帯果物です。甘みと酸味が調和した味が人気の果物です。"
  },
  {
    "name": "ラズベリー",
    "description": "赤い小さな実がたくさんついた香り高い果実です。ジャムやお菓子の材料によく使われます。"
  },
  {
    "name": "ブルーベリー",
    "description": "小さな青紫色の果実が房になっている果物です。抗酸化作用があり健康に良い果物です。"
  }
]

const fuseOptions = {
  keys: [ "title", "description" ]
};

const fuse = new Fuse(searchItems, fuseOptions);

const searchQuery = ref('');

const searchResults = computed(() => {
  if (!searchQuery.value) return [];
  return fuse.search(searchQuery.value).map(m => m.item);
});

</script>
<template>
  <main>
    <div class="search-container">
      <input
          type="text"
          v-model="searchQuery"
          placeholder="Search..."
          class="search-input"
      />
      <div v-if="searchResults.length" class="search-results">
        <h2>Search Results:</h2>
        <ul>
          <li v-for="(result, index) in searchResults" :key="index" class="search-result">
            <p><strong>Name:</strong> {{ result.name }}</p>
            <p><strong>Description:</strong> {{ result.description }}</p>
          </li>
        </ul>
      </div>
      <div v-else class="no-results">
        <p>No results found</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
.search-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.search-input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.search-results {
  margin-top: 20px;
}

.search-result {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
}

.no-results {
  margin-top: 20px;
  text-align: center;
  color: #666;
}
</style>