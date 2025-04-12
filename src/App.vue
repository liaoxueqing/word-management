<template>
  <div class="main">
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
import { ref } from 'vue'
import WordManagement from './components/WordManagement.vue'
import PoetryManagement from './components/PoetryManagement.vue'
import { ElTabs, ElTabPane } from 'element-plus'

const activeName = ref('first')
//todo 从文件读值
const words1 = ref([{text:'一',status:true},{text:'二',status:false},{text:'三',status:''}])
const words2 = ref([{text:'六',status:true}])
const poetries1 = ref(['静夜思'])
const poetries2 = ref(['春晓'])

const handleWordsUpdate = (wordsRef, updatedWords) => {
  // todo 修改值并写入文件
  if (wordsRef === 'words1') {
      words1.value = updatedWords
    } else if (wordsRef === 'words2') {
      words2.value = updatedWords
    }
}

</script>

<style>
.main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 60px;
}
</style>
