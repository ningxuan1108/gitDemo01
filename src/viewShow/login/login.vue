<template>
  <div class="wrapper">
      <div class="user">
          <label>用户名</label>
          <input type="text" placeholder="请输入用户名"/>
      </div>
      <div class="user">
            <label>密码</label>
           <input type="password" placeholder="请输入密码"/>
      </div>
      <div class="loginInfo">登录</div>
  </div>
</template>

<script>
export default {
  components:{},
  props:{},
  data(){
    return {
    }
  },
  watch:{
     $route: {
      handler: function(route) {
        console.log('获取参数列表',route);
        this.redirect = route.query && route.query.redirect
      },
      immediate: true
    }
  },
  computed:{},
  methods:{},
  created(){},
  mounted(){}
}
</script>
<style lang="scss" scoped>
.wrapper{}
.user{
    width: 500px;
    height: 60px;
    margin-top: 60px;
    margin-left: 120px;
    border-bottom: 1px solid red;
    display: flex;
    justify-content: space-between;
    align-items: center;
    label{
        width:30%;
    }
    input{
        width:65%;
        height:58px;
    }
}
.loginInfo{
    width: 500px;
    height: 60px;
    margin-top: 30px;
    margin-left: 120px;
    background-color: red;
    color: white;
    line-height: 60px;
    text-align: center;
}
</style>