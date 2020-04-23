<template>
  <el-card class="box-card" style="margin-left:8px;">
    <div slot="header" class="clearfix">
      <span>常用功能</span>
    </div>
    <el-row>
      <el-col :span="12">
        <el-card shadow="hover" class="spanDemo" @click.native="routerTo('用户管理')">
          <span><svg-icon icon-class="peoples" />用户管理</span>
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card shadow="hover" class="spanDemo" @click.native="routerTo('新闻动态')">
          <span><svg-icon icon-class="form" />新闻动态</span>
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card shadow="hover" class="spanDemo" @click.native="routerTo('作品展示')">
          <span><svg-icon icon-class="component" />作品展示</span>
        </el-card>
      </el-col>
      <el-col :span="12">
        <el-card shadow="hover" class="spanDemo" @click.native="routerTo('服务管理')">
          <span><svg-icon icon-class="international" />服务管理</span>
        </el-card>
      </el-col>
    </el-row>
  </el-card>
</template>

<script>
import { mapGetters } from 'vuex'
// import PanThumb from '@/components/PanThumb'
// import Mallki from '@/components/TextHoverEffect/Mallki'

export default {

  filters: {
    statusFilter(status) {
      const statusMap = {
        success: 'success',
        pending: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      statisticsData: {
        article_count: 1024,
        pageviews_count: 1024
      }
    }
  },
  computed: {
    ...mapGetters([
      'name',
      'avatar',
      'roles'
    ])
  },
  methods: {
    routerTo(flag) {
      switch (flag) {
        case '用户管理':
          this.$router.push('/userManagement/index')
          break
        case '新闻动态':
          this.$router.push('/news/index')
          break
        case '作品展示':
          this.$router.push('/gallery/index')
          break
        case '服务管理':
          this.$router.push('/serviceManagement/serviceManagement')
          break
        default:
          this.$router.push('/dashboard')
          break
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.box-card{
  .spanDemo{
    margin: 4px 4px;
    font-size: 16px;
  }
  .spanDemo:hover{
    background-color: #9fabb9;
  }
}
</style>
