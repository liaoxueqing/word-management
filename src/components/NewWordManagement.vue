<template>
  <el-row :wrap="true" :gutter="20" class="create-area">
    <el-col :xs="24" :sm="24" :md="8" :lg="6">
      <el-input
        v-model="newWords"
        :rows="3"
        type="textarea"
        placeholder="Please input"
      />
    </el-col>
    <el-col :xs="24" :sm="24" :md="8" :lg="6" class="action-row">
      <el-button type="primary" class="btn" @click="handleAddClick">增加</el-button>
      <el-button  class="btn" @click="handleExportClick">导出字库</el-button>
      <el-button  class="btn" @click="handleExportWordStatusClick">导出识字记录</el-button>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: 'WordManagement',

  props: {
    words: {
      type: Array,
      default: () => []
    },
    words2: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      newWords: ''
    }
  },
  methods: {
    handleAddClick() {
      this.$emit('update:newWords', this.newWords);
      this.newWords = ''
    },

    export(data, filename) {
      const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'})
      const url = URL.createObjectURL(blob)

      const a = document.createElement('a')
      a.href = url
      a.download = filename
      document.body.appendChild(a)
      a.click()
      document.body.removeChild(a)
    },
    // 导出字库
    handleExportClick() {
      const data = this.words.map(word => word.text).join("")
      this.export(data, `words-${new Date().toLocaleDateString()}.docx`)
    },

    // 导出字库
    handleExportWordStatusClick() {
      const data1 = this.words.map(word => {
        return `${word.text}${word.status ? '(✅)' : (word.status === '' ? '( )' : '(❌)')}`
      }).join(" ")
      const data2 = this.words2.map(word => {
        return `${word.text}${word.status ? '(✅)' : (word.status === '' ? '( )' : '(❌)')}`
      }).join(" ")
      this.export(data1, `航认字记录-${new Date().toLocaleDateString()}.docx`)
      this.export(data2, `皓皓认字记录-${new Date().toLocaleDateString()}.docx`)
    }
  }
}
</script>

<style scoped>
.action-row .btn {
  margin: 20px 20px 0 0;
}
</style>