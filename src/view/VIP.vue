<template>
    <div style="text-align: center">
      <v-top/>
      <h1 style="color: red; font-size: 40px; margin-top: 30px; margin-bottom: 20px;">
        最后一步，扫码即可开通VIP
      </h1>
      <h2 style="color: #ff20ed; margin-bottom: 30px;">只要9.99,全部功能即可解锁</h2>
      <div style="width: 80%; height: 600px; text-align: center; margin-left: 100px;">
        <div style="width: 40%; float: left; margin-left: 100px;" class="imgZFB">
          <!--<img src="../../image/支付宝收款.jpg"/>-->
        </div>
        <div class="imgWX" style="width: 40%; float: left; margin-left: 100px;">
        </div>
      </div>
    </div>
</template>

<script>
  import vtop from '../components/top.vue'
  export default {
    name: "VIP",
    components: {
      'v-top': vtop,
    },
  }
</script>

<style scoped>
  .imgZFB{
    width: 100%;
    height: 100%;
    background: url('../../image/支付宝收款.jpg') center center no-repeat;
    background-size: cover;
  }
  .imgWX{
    width: 100%;
    height: 100%;
    background: url('../../image/微信收款.jpg') center center no-repeat;
    background-size: cover;
  }
</style>
