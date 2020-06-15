<template>
  <div class="img">
    <div style="height: 20px; float: top;">
    </div>
    <div style="width: 450px; height: 670px; margin-left: 35%;background: azure; border-radius: 10px; align-content: center">
      <div style="height: 150px; font-size: 50px; line-height: 150px;">注册</div>
      <el-form ref="user" :model="user" style="margin-left: 20px; margin-right: 20px;">
        <el-form-item>
          <el-input v-model="user.phone" placeholder="手机号"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input type="password" v-model="user.password" placeholder="密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="user.uname" placeholder="姓名"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="user.username" placeholder="学号"></el-input>
        </el-form-item>
        <el-form-item label="性别">
          <el-radio-group v-model="user.usex">
            <el-radio label="男"></el-radio>
            <el-radio label="女"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item>
          <el-input v-model="user.school" placeholder="学校"></el-input>
        </el-form-item>
        <el-form-item label="我是:">
          <el-radio-group v-model="type">
            <el-radio label="老师" value="2"></el-radio>
            <el-radio label="学生" value="3"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submit" style="width: 310px">注册</el-button>
        </el-form-item>
        <router-link to='/login'>
          <a style="width: 50px; float: right; font-size: 13px;"> 去登录</a>
        </router-link>
        <div style="width: 100px;height: 30px; margin-left: 300px; font-size: 13px;">
          已有账号?
        </div>
      </el-form>
    </div>
  </div>
</template>

<script>
    import * as qs from "qs";

    export default {
      data(){
        return{
          user: {},
          type: '',
        }
      },

      methods:{
        submit(){
          if(this.type ==="老师"){
            debugger
            console.log(this.user)
            this.$axios.get('http://127.0.0.1:8080/loginUp/addTeacher?user=id=1&'+qs.stringify(this.user))
            //   {
            //   method: 'post',
            //   url: 'http://127.0.0.1:8080/loginUp/addTeacher',
            //   data: JSON.stringify(this.user)
            // })
          .then(res =>{
                console.log(this.user)
                console.log(this.type)
                console.log(res)
                alert("注册成功，请牢记你的密码")
                this.$router.push('/');
              })
              .catch(err=>{
                alert("该学号已注册！");
                console.log(err);
              });
          }else if(this.type === "学生"){
            this.$axios.get('http://127.0.0.1:8080/loginUp/addStudent?user=id=1&'+qs.stringify(this.user))
              .then(res =>{
                console.log(this.user)
                console.log(this.type)
                console.log(res)
                alert("注册成功，请牢记你的密码")
                this.$router.push('/');
              })
              .catch(err=>{
                console.log(this.user);
                alert("该学号已注册！");
                console.log(err);
              });
          }
        }
      }
    }
</script>

<style scoped>
  .img{
    width: 100%;
    height: 100%;
    background: url('../../image/signUpBackground.jpg') center center no-repeat;
    background-size: cover;
  }
</style>
