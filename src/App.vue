<template>
  <div class="main">
  <el-tabs v-model="activeName">
    <el-tab-pane label="航认字" name="first">
      <WordManagement :words="words1"
                      @update:words="(updatedWords) => handleWordsUpdate('words1', updatedWords)"
      ></WordManagement>
    </el-tab-pane>
    <el-tab-pane label="皓皓认字" name="second">
      <WordManagement :words="words2"
                      @update:words="(updatedWords) => handleWordsUpdate('words2', updatedWords)"
      ></WordManagement>
    </el-tab-pane>
<!--    <el-tab-pane label="航古诗背诵" name="third">-->
<!--      <PoetryManagement :poetryList="poetryList1"></PoetryManagement>-->
<!--    </el-tab-pane>-->
<!--    <el-tab-pane label="皓皓古诗背诵" name="fourth">-->
<!--      <PoetryManagement  :poetryList="poetryList2"></PoetryManagement>-->
<!--    </el-tab-pane>-->
    <el-tab-pane label="管理字库" name="fifth">
      <NewWordManagement  :words="words1" :words2="words2"  @update:newWords="addWords"></NewWordManagement>
    </el-tab-pane>
  </el-tabs>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import WordManagement from './components/WordManagement.vue'
// import PoetryManagement from './components/PoetryManagement.vue'
import NewWordManagement from './components/NewWordManagement.vue'
import { ElTabs, ElTabPane } from 'element-plus'

const activeName = ref('first')
//todo 从文件读值
const words1 = ref([])
const words2 = ref([])
// const poetryList1 = ref(['静夜思'])
// const poetryList2 = ref(['春晓'])

onMounted(() => {
  words1.value = JSON.parse(localStorage.getItem('first')) || [];
  words2.value = JSON.parse(localStorage.getItem('second')) || [];
})

const handleWordsUpdate = (wordsRef, updatedWords) => {
  // todo 修改值并写入文件
  if (wordsRef === 'words1') {
      words1.value = updatedWords
      localStorage.setItem('first', JSON.stringify(updatedWords));
    } else if (wordsRef === 'words2') {
      words2.value = updatedWords
      localStorage.setItem('second', JSON.stringify(updatedWords));

  }
}

const addWords = (newWords) => {
  if (!newWords.trim()) return; // 空值检查

  // 分割并处理新单词
  const newWordsArray = newWords
  .split('').filter(word => word.trim() !== '');

  // 去重逻辑
  const existingWords = new Set(words1.value.map(item => item.text));

  // 过滤掉已存在的单词
  const uniqueNewWords = newWordsArray.filter(word =>
    !existingWords.has(word)
  );
  if (!uniqueNewWords.length) {
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
}

</script>

<style>
.main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 60px;
}
</style>
