<template>
  <div class="main">
  <el-tabs v-model="activeName" @tab-click="handleClick">
    <el-tab-pane label="航认字" name="first">
      <WordManagement :words="words1"></WordManagement>
    </el-tab-pane>
    <el-tab-pane label="皓皓认字" name="second">
      <WordManagement :words="words2"></WordManagement>
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

const words1 = ref(['一', '二', '三', '四', '五'])
const words2 = ref(['六', '七', '八', '九', '十'])
const poetries1 = ref(['静夜思'])
const poetries2 = ref(['春晓'])

</script>

<style>
.main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 60px;
}
</style>
