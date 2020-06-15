<template>
  <div>
    <div style="box-shadow: 0 0 10px #ccc; height: 72px; z-index: 3">
        <a style="width:118px; height: 30px; font-size: 50px; float: left;
                    margin-left: 100px; margin-top: 20px; " class="img" @click="$router.go(-1)">
        </a>
      <span style="font-size: 25px; line-height: 72px;">全国大学都在用的课堂管理软件</span>
      <el-button type="warning" round style="float: right; margin-right: 100px; margin-top: 15px;"
                 @click="logout()">退出</el-button>
    </div>
  </div>
</template>

<script>
    export default {
      name: "v-top",
      methods:{
        logout(){
          this.$confirm("确认退出吗？").then(_=>{
            //注销操作
            this.$axios.post('api/logout').then(_=>{
              //退出并跳转到登录页面
              this.$router.push('/login');
            }).catch(_=>{

            });
          }).catch(_=>{

          });
        },
      }
    }
</script>

<style scoped>
  .img{
    width: 100%;
    height: 100%;
    background: url('../../image/logo.jpg') center center no-repeat;
    background-size: cover;
  }
</style>
