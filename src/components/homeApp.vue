<template>
  <div>
    Home组件！
    <el-row>
      <el-button type="danger" round @click="tuiChu">退出</el-button>
    </el-row>
  </div>
</template>

<script>
export default {
  methods: {
    tuiChu() {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
  },
}
</script>

<style lang="less" scoped>
</style>