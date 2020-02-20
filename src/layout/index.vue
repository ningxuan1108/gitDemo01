<template>
<!-- :class="classObj" -->
  <div  class="app-wrapper">
      <!-- 侧边栏组件 -->
      <side-bar class="sidebar-container"></side-bar>

  </div>
</template>

<script>
import { SideBar } from './components';
export default {
  components:{
    'side-bar':SideBar
  },
  props:{},
  data(){
    return {
    }
  },
  watch:{},
  computed:{
    // 实时获取 router 列表
   
  },
  methods:{},
  created(){},
  mounted(){}
}
</script>
<style lang="scss" scoped>
// @import "../styles/mixin.scss";
// @import "../styles/variables.scss";
  @import "~@/styles/mixin.scss";
  @import "~@/styles/variables.scss";
.app-wrapper{
  @include clearfix;
  width: 100%;
  height: 100%;
  position: relative;
  &.mobile.openSidebar{
      position: fixed;
      top: 0;
    }
}
</style>