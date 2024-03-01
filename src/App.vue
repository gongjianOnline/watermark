<template>
  <div>
    <Watermark targeContent="龚箭前端"></Watermark>
    <div class="container">
      <button @click="handleClick">测试一下事件被覆盖</button>
    </div>
  </div>
</template>

<script lang="ts" setup>

import Watermark from "./components/Watermark.vue";
const handleClick = ()=>{
  alert("不影响鼠标等交互事件")
}




</script>

<style scoped>
div{
  width: 100vw;
  height: 100vh;
}
.container{
  width: 100%;
  height: 100%;
}
</style>