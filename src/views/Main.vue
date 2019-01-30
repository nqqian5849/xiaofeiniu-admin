<template>
  <div class="main">
    <el-container>
      <!--左侧边栏-->
      <el-aside width="150px">左侧</el-aside>
      <el-container>
        <!--顶部信息-->
        <el-header height="60px">111</el-header>
        <!--主体部分-->
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  export default {
    //检查是否有登录
    beforeCreate() {
      //组件创建之前先检查是否已经登录
      if(!this.$store.state.adminName){
        this.$router.push('/login');//未登录则跳转
      }
    },


  }
</script>
