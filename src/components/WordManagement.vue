<template>
  <div class="words-management">
    <header>
      <div>总数{{ words.length }} 未检查{{words.length-recognizedCount-unrecognizedCount}}</div>
      <div>认识{{recognizedCount}} 不认识{{unrecognizedCount}}</div>
    </header>
    <div class="word-list-area" style="height : calc(100vh - 163px);">
      <el-row :gutter="20" :wrap="true">
        <el-col
          v-for="(word, index) in words"
          :key="index"
          :xs="12"
          :sm="6"
          :md="4"
          :lg="3"
          :style="{ marginBottom: '20px' }"
        >
          <el-card shadow="hover"
                  class="box-card"
                  :body-class="word.status ? 'recognized' : (word.status === '' ? 'init' : 'unrecognized')">
            <div class="word-item">
              <div>{{ word.text }}</div>
              <div style="display: flex;">
                <el-checkbox-button
                  :model-value="word.status === true"
                                    @change="() => updateStatus(word, index, true)">✔️</el-checkbox-button>
                <el-checkbox-button
                  :model-value="word.status === false"
                  @change="() => updateStatus(word, index, false)">❌</el-checkbox-button>
              </div>
            </div>
          </el-card>
        </el-col>
    </el-row>
  </div>
  </div>
</template>

<script>
export default {
  name: 'WordManagement',
  props: {
    words: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    recognizedCount() {
      return this.words.filter(word => word.status === true).length;
    },
    unrecognizedCount() {
      return this.words.filter(word => word.status === false).length;
    },
  },
  methods: {
    updateStatus(word, index, newStatus) {
      const updatedWords = [...this.words];

      if (newStatus === updatedWords[index].status) {
        updatedWords[index].status = '';
      } else {
        updatedWords[index].status = newStatus;
      }

      this.$emit('update:words', updatedWords);
    }
  }
}
</script>

<style scoped>
.words-management {
  padding: 0;
}
.words-management header {
  font-size: 24px;
}
.word-list-area {
  overflow-y: auto;
}

.word-item {
  font-size: 32px;
  display: flex;
  flex-direction: column;
  align-items: center;  /* 垂直居中 */
  justify-content: center;  /* 水平居中 */
}
:deep(.init) {
  background-color: #f5f7fa;
}
:deep(.recognized) {
  background-color: #67c23a;
}
:deep(.unrecognized) {
  background-color: #ff6666;
}
</style>