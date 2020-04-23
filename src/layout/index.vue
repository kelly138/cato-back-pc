<template>
  <div :class="classObj" class="app-wrapper">
    <div class="app-header">
      <span class="user-logo">
        <el-link>
          <i class="el-icon-user-solid" />
        </el-link>
      </span>
      <span class="user-name">
        系统管理员
      </span>
      <span class="user-out">
        <el-link @click.native="logout">
          <i class="el-icon-switch-button" />
        </el-link>
      </span>
    </div>
    <div v-if="device==='mobile'&&sidebar.opened" class="drawer-bg" @click="handleClickOutside" />
    <sidebar class="sidebar-container" />
    <div :class="{hasTagsView:needTagsView}" class="main-container">
      <div :class="{'fixed-header':fixedHeader}">
        <navbar />
        <!-- <tags-view v-if="needTagsView" /> -->
      </div>
      <app-main />
      <right-panel v-if="showSettings">
        <settings />
      </right-panel>
    </div>
  </div>
</template>

<script>
import RightPanel from '@/components/RightPanel'
import { AppMain, Navbar, Settings, Sidebar } from './components'
import { mapState } from 'vuex'

export default {
  name: 'Layout',
  components: {
    AppMain,
    Navbar,
    RightPanel,
    Settings,
    Sidebar
    // TagsView
  },
  computed: {
    ...mapState({
      sidebar: state => state.app.sidebar,
      device: state => state.app.device,
      showSettings: state => state.settings.showSettings,
      needTagsView: state => state.settings.tagsView,
      fixedHeader: state => state.settings.fixedHeader
    }),
    classObj() {
      return {
        hideSidebar: !this.sidebar.opened,
        openSidebar: this.sidebar.opened,
        withoutAnimation: this.sidebar.withoutAnimation,
        mobile: this.device === 'mobile'
      }
    }
  },
  methods: {
    handleClickOutside() {
      this.$store.dispatch('app/closeSideBar', { withoutAnimation: false })
    },
    async logout() {
      await this.$store.dispatch('user/logout')
      this.$router.push(`/login?redirect=${this.$route.fullPath}`)
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "~@/styles/mixin.scss";
  @import "~@/styles/variables.scss";

  .app-wrapper {
    @include clearfix;
    position: relative;
    height: 100%;
    width: 100%;

    &.mobile.openSidebar {
      position: fixed;
      top: 0;
    }
    .app-header{
      text-align: right;
      // font-size: 35px;
      height: 60px;
      line-height: 60px;
      width: 100%;
      background: url(../assets/images/banner.jpg) 50% no-repeat;
      // background-color: #5a5e66;
      background-size: 100% 100%;
      margin-bottom: 0px;
      z-index: 1002;
      .el-icon-user-solid{
        font-size: 35px;
        height: 60px;
        color: #fff;
        line-height: 60px;
        cursor:default;
      }
      .user-name{
        color: #fff;
        margin: auto 10px;
        cursor:default;
      }
      .user-out{
        margin-right:10px;
      }
      .el-icon-switch-button{
        font-size: 35px;
        height: 60px;
        color: #fff;
        line-height: 60px;
      }
    }
  }

  .drawer-bg {
    background: #000;
    opacity: 0.3;
    width: 100%;
    top: 0;
    height: 100%;
    position: absolute;
    z-index: 999;
  }

  .fixed-header {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 9;
    width: calc(100% - #{$sideBarWidth});
    transition: width 0.28s;
  }

  .hideSidebar .fixed-header {
    width: calc(100% - 54px)
  }

  .mobile .fixed-header {
    width: 100%;
  }
</style>
