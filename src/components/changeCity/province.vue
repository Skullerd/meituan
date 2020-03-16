<template>
  <div>
    <span class="name">按省份选择：</span>
    <m-select
      :list="provinceList"
      title="省份"
      :value="province"
      :showWrapperActive="provinceActive"
      @change_active="changeProvinceActive"
      @change="changeProvince"
      :className="'province'"
    />
    <m-select
      :list="cityList"
      title="城市"
      :value="city"
      :showWrapperActive="cityActive"
      @change_active="changeCityActive"
      @change="changeCity"
      :disabled="cityDisabled"
      :className="'city'"
    />
    <span>直接搜索：</span>
    <el-select
      v-model="searchWord"
      filterable
      remote
      reserve-keyword
      placeholder="请输入关键词"
      :remote-method="remoteMethod"
      :loading="loading"
    >
      <el-option v-for="item in searchList" :key="item" :label="item" :value="item"></el-option>
    </el-select>
  </div>
</template>
<script>
import MSelect from './select.vue'
import api from '@/api/index.js'
export default {
  data () {
    return {
      provinceList: [],
      province: '省份',
      city: '城市',
      cityList: [],
      cityActive: false,
      provinceActive: false,
      searchList: ['哈尔滨', '上海', '佛山', '广州', '北京'],
      searchWord: '',
      loading: false,
      cityDisabled: true
    }
  },
  components: {
    MSelect
  },
  created () {
    api.getProvinceList().then(res => {
      this.provinceList = res.data.data.map(item => {
        item.name = item.provinceName
        return item
      })
    })
  },
  methods: {
    changeProvinceActive (flag) {
      this.provinceActive = flag

      if (flag) {
        this.cityActive = false
      }
    },
    changeCityActive (flag) {
      this.cityActive = flag
      if (flag) {
        this.provinceActive = false
      }
    },
    changeCity (value) {
      this.city = value.name
      this.$store.dispatch('setPosition', value)
      this.$router.push({ name: 'index' })
    },
    changeProvince (value) {
      this.province = value.name
      this.cityDisabled = false
      this.cityList = value.cityInfoList
    },
    remoteMethod (val) {
      // 向后端发送请求
    }
  }
}
</script>

<style lang="scss">
@import "@/assets/css/changecity/iselect.scss";
</style>
