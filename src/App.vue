<template>
  <div class="main">
    <el-row :wrap="true" :gutter="20" class="create-area">
      <el-col :xs="24" :sm="12" :md="6" :lg="4">
        <el-input
        v-model="newWords"
        :rows="3"
        type="textarea"
        placeholder="Please input"
      />
      </el-col>
      <el-col :xs="24" :sm="12" :md="6" :lg="4">
        <el-button type="primary" @click="addWords">增加</el-button>
      </el-col>
    </el-row>
  <el-tabs v-model="activeName">
    <el-tab-pane label="航认字" name="first">
      <WordManagement :words="words1"
                      @update:words="(updatedWords) => handleWordsUpdate('words2', updatedWords)"
      ></WordManagement>
    </el-tab-pane>
    <el-tab-pane label="皓皓认字" name="second">
      <WordManagement :words="words2"
                      @update:words="(updatedWords) => handleWordsUpdate('words2', updatedWords)"
      ></WordManagement>
    </el-tab-pane>
    <el-tab-pane label="航古诗背诵" name="third">
      <PoetryManagement :poetryList="poetries1"></PoetryManagement>
    </el-tab-pane>
    <el-tab-pane label="皓皓古诗背诵" name="fourth">
      <PoetryManagement  :poetryList="poetries2"></PoetryManagement></el-tab-pane>
  </el-tabs>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import WordManagement from './components/WordManagement.vue'
import PoetryManagement from './components/PoetryManagement.vue'
import { ElTabs, ElTabPane } from 'element-plus'

const activeName = ref('first')
//todo 从文件读值
const words1 = ref([])
const words2 = ref([])
const newWords = ref('')
const poetries1 = ref(['静夜思'])
const poetries2 = ref(['春晓'])

onMounted(() => {
  words1.value = JSON.parse(localStorage.getItem('first')) || [];
  words2.value = JSON.parse(localStorage.getItem('second')) || [];
})

const handleWordsUpdate = (wordsRef, updatedWords) => {
  // todo 修改值并写入文件
  if (wordsRef === 'words1') {
      words1.value = updatedWords
    } else if (wordsRef === 'words2') {
      words2.value = updatedWords
    }
}

const addWords = () => {
  if (!newWords.value.trim()) return; // 空值检查

  // 分割并处理新单词
  const newWordsArray = newWords.value
  .split('');

  // 去重逻辑
  const existingWords = new Set(words1.value.map(item => item.text));

  // 过滤掉已存在的单词
  const uniqueNewWords = newWordsArray.filter(word =>
    !existingWords.has(word)
  );
  if (!uniqueNewWords.length) {
    newWords.value = '';
    return;
  }

  // 创建新单词对象数组
  const newWordObjects = uniqueNewWords.map(word => ({
    text: word,
    status: ''
  }));

  // 更新数据
  const updatedWords1 = [...words1.value, ...newWordObjects];
  const updatedWords2 = [...words2.value, ...newWordObjects];

  words1.value = updatedWords1;
  words2.value = updatedWords2;

  // 保存到本地存储
  localStorage.setItem('first', JSON.stringify(updatedWords1));
  localStorage.setItem('second', JSON.stringify(updatedWords2));
  newWords.value = '';
}

</script>

<style>
.main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 60px;
}
</style>
