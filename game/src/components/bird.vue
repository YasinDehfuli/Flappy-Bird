<template>
  <img src="@/assets/bird.png" alt="player" :style="'top:'+top+'px'">
</template>

<script>
export default {
  name: "bird",
  props:['top']
}
</script>

<style scoped>
  img{
    height: 100px;
    position: absolute;
    left: 250px;
    top: 0;
    transition: 300ms;
  }
</style>