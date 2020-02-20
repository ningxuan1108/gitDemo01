<template>
  <div  v-if="!item.hidden">
    <template v-if="hasOneShowingChild(item.children,item) && (!onlyOneChild.children||onlyOneChild.noShowingChildren)">
      <app-link v-if="onlyOneChild.meta" :to="resolvePath(onlyOneChild.path)">
        <el-menu-item :index="resolvePath(onlyOneChild.path)" :class="{'submenu-title-noDropdown':!isNest}">
          <app-item :icon="onlyOneChild.meta.icon||(item.meta&&item.meta.icon)" :title="onlyOneChild.meta.title" ></app-item>
        </el-menu-item>
      </app-link>
    </template>
     <el-submenu v-else ref="subMenu" :index="resolvePath(item.path)" popper-append-to-body>
      <template slot="title">
        <app-item v-if="item.meta" :icon="item.meta && item.meta.icon" :title="item.meta.title" ></app-item>
      </template>
      <sidebar-item
        v-for="child in item.children"
        :key="child.path"
        :is-nest="true"
        :item="child"
        :base-path="resolvePath(child.path)"
        class="nest-menu"
      />
    </el-submenu>
      
  </div>
</template>

<script>
import path from 'path';
import AppItem from './Item';
import AppLink from './Link'
import { isExternal } from '../../../utils/validate';
export default {
  name: 'SidebarItem',
  components:{
      'app-item':AppItem,
      'app-link':AppLink
  },
  props:{
    item: {
      type: Object,
      required: true
    },
    isNest: {
      type: Boolean,
      default: false
    },
    basePath: {
      type: String,
      default: ''
    }
  },
  data(){
    return {
        onlyOneChild:null
    }
  },
  watch:{},
  computed:{},
  methods:{
      // 侧边栏 递归组件
     // 默认数组
     // 一层一层递归 如果有就存储  如果没有就展示空数组 []
      hasOneShowingChild(children = [],parent){
        const showingChildren = children.filter(item => {
            if (item.hidden) {
                return false
            } else {
                // Temp set(will be used if only has one showing child)
                this.onlyOneChild = item
                return true
            }
        }) 
        // 判断数组长度 
        if(showingChildren.length ==1){
            return true;
        }
        if(showingChildren.length==0){
            this.onlyOneChild = { ... parent, path: '', noShowingChildren: true};
            return true;
        }
        return false;
      },
      resolvePath(routePath){
        if (isExternal(routePath)) {
            return routePath
        }
        if (isExternal(this.basePath)) {
            return this.basePath
        }
        return path.resolve(this.basePath, routePath)
      }
  },
  created(){},
  mounted(){}
}
</script>
<style lang="scss" scoped>
</style>