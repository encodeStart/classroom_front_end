<template>
  <div>
    <v-top/>
    <div style="float: left; height: 30px; width:100%; z-index:1;">
        <span style="margin-left: 100px; margin-top: 15px; font-size: 15px; float: left;">
          <a @click="jumpToMain">全部课程</a>
        </span>
    </div>
    <div style="margin-left: 100px; height: 200px; width: 90%; margin-top: 50px;
          border-top-left-radius: 8px; border-top-right-radius: 8px;" class="imgCard">
      <div style="width: 100%; height: 50px;"></div>
      <span style="color: white; font-size: 50px;">{{name}}</span>
    </div>
    <div style="margin-left: 100px; margin-right: 54px;">
      <el-menu router="/coursePage" :default-active="activeIndex" class="el-menu-demo"
               mode="horizontal" @select="handleSelect"
               style="background: rgba(241,243,244,1);">
        <el-menu-item index=workList style="margin-left: 20px;">
          全部作业
        </el-menu-item>
        <el-submenu style="margin-left: 500px;">
          <template slot="title">教学团队</template>
          <el-menu-item index="teamOfTeacher">老师</el-menu-item>
          <el-menu-item index=teamOfStudent>学生</el-menu-item>
        </el-submenu>
        <el-menu-item index=scoreList style="margin-left: 500px;">
          <a target="_blank">成绩详情</a>
        </el-menu-item>
      </el-menu>
    </div>

    <!--显示作业等div框-->
    <div style="margin-top: 20px; margin-left: 100px; margin-right: 55px;">
      <router-view/>
    </div>
  </div>
</template>

<script>
  import scoreList from '@/view/coursePage/scoreList.vue'
  import teamOfStudent from '@/view/coursePage/teamOfStudent.vue'
  import teamOfTeacher from '@/view/coursePage/teamOfTeacher.vue'
  import workList from '@/view/coursePage/workList.vue'
  import vtop from '../components/top.vue'

  export default {
    name: "coursePage",
    props:{
      active:{
        type:String,
        required: true
      }
    },
    components: {
      scoreList,
      teamOfStudent,
      teamOfTeacher,
      workList,
      'v-top': vtop,
    },
    data(){
      return{
        name:'',
        uid:'',
      }
    },
    methods: {
      handleSelect(key, keyPath) {
        this.$emit('update:active',key)
      },

      jumpToMain(){
        this.$axios.get('api/teacher/getUserByUid?uid='+this.uid)
          .then(res=>{
            if (res.data.roles[0].id === 2){
              this.$router.push({name:'mainTeacher',params:{uid:this.uid}})
            }else if(res.data.roles[0].id === 3){
              this.$router.push({name:'mainStudent',params:{uid:this.uid}})
            }
          }).catch(err=>{
            console.log(err);
        })
        
      },

      getCourse(cid){
        this.$axios.get('api/teacher/getCourseByCid?cid='+cid)
          .then(res=>{
            this.name = res.data.name;
          }).catch(err=>{
          console.log(err);
        })
      }

    },
    mounted(){
      if (this.$route.params.cid !== undefined){
        this.getCourse(this.$route.params.cid);
        this.uid = this.$route.params.uid;
      }
    }
  }
</script>

<style scoped>
  .imgCard{
    width: 100%;
    height: 100%;
    background: url('../../image/CardBackground.jpg') center center no-repeat;
    z-index: -10;
    background-size: cover;
  }
  .img{
    width: 100%;
    height: 100%;
    background: url('../../image/logo.jpg') center center no-repeat;
    background-size: cover;
  }

</style>
