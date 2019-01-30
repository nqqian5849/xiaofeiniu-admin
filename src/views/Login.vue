<template>
  <div class="login">
    <el-card class="xfn-login-card">
      <div slot="header">管理员登录</div>
      <div>
        <el-form label-width="85px">
          <el-form-item label="管理员名：" >
            <el-input v-model="formData.aname" placeholder="请输入管理员名"></el-input>
          </el-form-item>
          <el-form-item label="登录密码：">
            <el-input v-model="formData.apwd" placeholder="请输入管理员密码"></el-input>
          </el-form-item>
          <el-form-item>
          <!--除了el-button vue本身不允许自定属性监听原生dom 必须加native-->
            <el-button type="primary" @click.native="doLogin">登录</el-button>
            <el-button @click.native="doCancel">取消</el-button>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>

<script>
  export default {
    data(){//普通组件模型数据
      return {
        formData:{//表单中用户输入的两个数据
          aname:'admin',
          apwd:'123456'
        }
      }
    },
    methods:{
      doLogin(){//执行登陆
        var url = this.$store.state.globalSettings.apiUrl+`/admin/login/${this.formData.aname}/${this.formData.apwd}`;
        this.$axios.get(url).then((res)=>{
          // console.log(res.data);
          if(res.data.code==200){//登录成功
          this.$store.commit('setAdminName',this.formData.aname)
            this.$router.push('/main')
          }else{//登录失败
            this.$alert("用户名或密码有误！","登录失败",{type:'error'}).then(()=>{}).catch(()=>{});
          }
        }).catch((err)=>{
          console.log(err)
        })
        console.log(url)
      },
      doCancel(){//清除用户当前输入
        this.formData.aname=''
        this.formData.apwd=''
      }
    },

  }
</script>

<style lang="scss">
  .xfn-login-card{
    width:450px;
    margin:150px auto;
    .el-card__header{
      text-align:center;
      font-size:1.2em;
    }
  }
</style>