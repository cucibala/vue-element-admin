<template>
  <div class="app-container documentation-container">
    <el-row>
      <el-col :span="24">
        <el-tabs v-model="activeName" type="border-card" @tab-click="handleClick">
          <el-tab-pane label="java" name="java" class="java">
            <pre v-highlightjs v-html="java" />
          </el-tab-pane>
          <el-tab-pane label="php" name="php" class="php">
            <pre v-highlightjs v-html="php" />
          </el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { queryArticle } from '@/api/article.js'
const hljs = require('highlight.js')

export default {
  name: 'Documentation',
  data() {
    return {
      activeName: 'java',
      java: '',
      php: ''
    }
  },
  mounted() {
    this.refreshArticle()
  },
  methods: {
    refreshArticle() {
      queryArticle(this.activeName).then(response => {
        const { data } = response
        const { value } = hljs.highlight(this.activeName, data)
        this[this.activeName] = value
      })
    },
    handleClick(tab, event) {
      this.refreshArticle()
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
