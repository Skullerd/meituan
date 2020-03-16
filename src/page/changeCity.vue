<template>
  <div class="page-changeCity">
    <el-row>
      <province />
    </el-row>
    <el-row>
      <hot title="热门城市" :list="hotList" />
    </el-row>
    <el-row>
      <hot title="最近访问" :list="rencentList" />
    </el-row>
    <el-row>
      <Category />
    </el-row>
  </div>
</template>

<script>
import Province from '@/components/changeCity/province.vue'
import Hot from '@/components/changeCity/hot.vue'
import Category from '@/components/changeCity/category.vue'
import api from '@/api/index.js'
export default {
  data () {
    return {
      hotList: [],
      rencentList: []
    }
  },
  created () {
    api.getHotCity().then(res => {
      this.hotList = res.data.data.map(item => item.name)
    })
    api.getRecentsCity().then(res => {
      this.rencentList = res.data.data.map(item => item.name)
    })
  },
  components: {
    Province,
    Hot,
    Category
  }
}
</script>
