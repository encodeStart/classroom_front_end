<template xmlns="http://www.w3.org/1999/html">
  <div class="img1">
    <div style="height: 100px; float: top;">
    </div>
    <div style="width: 400px; height: 385px; margin-left: 37%;background: azure; border-radius: 10px;">
      <div style="height: 150px; font-size: 50px; line-height: 150px;">账号登录</div>
        <el-form ref="user" :model="user" >
          <el-form-item>
            <el-input v-model="user.username" style="width:340px; min-height: 50px;" placeholder="账号"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input type="password" v-model="user.password" style="width:340px; min-height: 50px;" placeholder="密码"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submit" style="width: 310px">登录</el-button>
          </el-form-item>
          <router-link to='/LoginUp'>
            <a style="width: 50px; float: right; margin-right: 35px;"> 去注册</a>
          </router-link>
          <div style="width: 100px;height: 30px; margin-left: 240px;">
            还没有账号?
          </div>
        </el-form>
    </div>
  </div>
</template>

<script>
import * as qs from "qs";

export default {
    data() {
      return {
        type: '',
        user: {},
        username: '',
        password: '',
      }
  },
  methods: {
    submit() {
      this.login();
    },

    login() {
      console.log(qs.stringify(this.user))
      this.$axios
        .post("api/login", qs.stringify(this.user), {
          headers: {
            'Content-Type':'application/x-www-form-urlencoded',
            }
        })
        .then(res => {
          this.user.uid = res.data.msg.uid;
          this.user.uname = res.data.msg.uname;
          this.type = res.data.msg.roles[0].id;
          console.log(this.user.uid)
          console.log(this.type)
          alert("登录成功");
          this.jumpToList()
      })
      .catch(err => {
        alert(err.msg);
        console.log(err);
      });
    },
     jumpToList() {
      if ((this.type === 2)){
        alert("欢迎您,"+this.user.uname[0]+"老师")
        this.$router.push({name: 'mainTeacher',params:{uid:this.user.uid}})
      }else if((this.type === 3)){
        alert(this.user.uname+"同学,你好")
        this.$router.push({name: 'mainStudent', params:{uid: this.user.uid}})
      }else {
        alert("本系统暂未设置管理员，请与开发人员联系")
      }
    }
  },

}
</script>
<style scoped>
  .img1{
    width: 100%;
    height: 100%;
    background: url('../../image/loginBackground.jpg') center center no-repeat;
    background-size: cover;
  }

</style>
