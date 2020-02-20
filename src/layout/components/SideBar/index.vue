<template>
   <div :class="{'has-logo':showLogo}">
    <!-- <logo v-if="showLogo" :collapse="isCollapse" /> -->
    <!-- 侧边栏展示信息 -->
     <!-- :default-active="activeMenu" -->
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-menu
       :default-active="activeMenu"
        :collapse="isCollapse"
        background-color="#304156"
        text-color="#409EFF"
        :unique-opened="false"
        active-text-color="#f4f4f5"
        :collapse-transition="false"
        mode="vertical"
      >
        <slide-bar v-for="route in routes" :key="route.path" :item='route' :base-path="route.path"></slide-bar>
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import slideBar from './sideBarItem';
export default {
  components:{
      'slide-bar':slideBar
  },
  props:{},
  data(){
    return {
    }
  },
  watch:{},
  computed:{
    ...mapGetters([
        'sidebar'
    ]),
    routes() {
      return this.$router.options.routes
    },
    isCollapse(){
        return !this.sidebar.opened;
    },
    showLogo(){
        return this.$store.state.settings.sidebarLogo
    },
    activeMenu() {
      const route = this.$route;
      const { meta, path } = route
      if (meta.activeMenu) {
        return meta.activeMenu
      }
      return path
    },
  },
  methods:{},
  created(){},
  mounted(){}
}
</script>
<style lang="scss" scoped>
</style>