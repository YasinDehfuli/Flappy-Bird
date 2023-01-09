<template>
  <div id="jimi" :style="styles">
    &nbsp;
  </div>
</template>

<script>
export default {
  name: "jimmy",
  data:function () {
    return{
      left: 100,
    }
  },
  mounted() {
    let self = this;
    setInterval(function () {
      self.left-=3;
    },300);
  },
  props: ['dire', 'h'],
  computed: {
    styles: function () {
      let txt = 'height:' + this.h + 'px;'
      if (this.dire == 'up'){
        txt +='top:0;'
      }else{
        txt +='bottom:0;'
      }
      txt +='left:'+this.left+'%;';
      return txt;
    }
  }
}
</script>

<style scoped>
#jimi {
  min-height: 10px;
  width: 120px;
  position: fixed;
  left: 100%;
  border: 5px solid rgba(0,255,53,1);
  background: linear-gradient(90deg, rgba(0,255,53,1) 0%, rgba(0,134,27,1) 18%, rgba(0,113,23,1) 75%, rgba(0,255,53,1) 100%);
  transition: 300ms ;
  transition-timing-function: linear;
}
</style>