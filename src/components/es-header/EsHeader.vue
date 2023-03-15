<template>
  <div class="head-container" :style="{'background-color':backgroundColor, color:color, fontSize:fontSize + 'px'}">{{title}}</div>
</template>

<script>

 export default {
  name:'EsHeader',
  props:{
    title:{
        type:String,
        default:'es-header'
    },
    backgroundColor:{
        type:String,
        default:'#0376ca'
    },
    color:{
        type:String,
        default:'White'
    },
    fontSize:{
        type:Number,
        default:12
    }
  }
 }

</script>

<style scoped>
.head-container {
    position: fixed;
    top: 0;
    left: 0;
    height: 45px;
    width: 100%;
    text-align: center;
    line-height: 45px;
    z-index: 999;
}

</style>