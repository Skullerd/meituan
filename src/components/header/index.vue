<template>
  <div class="m-header">
    <el-row>
      <top-bar />
    </el-row>
    <el-row style="box-shadow: 0 2px 27px 0 rgba(0,0,0,0.10);">
      <search-bar />
    </el-row>
  </div>
</template>

<script>
import topBar from './topBar.vue'
import searchBar from './searchBar'

export default {
  components: {
    topBar,
    searchBar
  }
}
</script>

<style lang="scss">
@import "@/assets/css/public/header/index.scss";
</style>
