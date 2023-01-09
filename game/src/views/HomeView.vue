<template>
  <div>
    <span v-for="n in health" > ❤️</span>
    <span style="float: right">{{time}}</span>
    <h1 v-if="health <= 0">
      Game over
    </h1>
    <bird :top="up"></bird>
    <div v-for="o in ops">
      <j class="op" :dire="o.dir" :h="o.h"></j>
      <j class="op" :dire="o.dir === 'up'?'down':'up'" :h="640 - o.h"></j>
    </div>
  </div>
</template>

<script>

import bird from '../components/bird.vue'
import j from '../components/jimmy.vue'

var int1;
var int2;

export default {
  name: "HomeView",
  components: {bird, j},
  data: function () {
    return {
      posX: 0,
      health: 3,
      up: 300,
      time: 0,
      ops: [{h: 350,dir:'up'}],
    }
  },
  mounted() {
    let self = this;

    document.addEventListener('keyup', function (e) {
      if (e.key == ' ') {
        self.up -= 150;
      }

      if (e.key == 'Escape'){

      }
      // console.log(e.key);
    });

    int1 = setInterval(function () {
      let dir = self.rnd(0, 10) % 2 == 0 ? 'up' : 'down';
      let h = self.rnd(200,600);
      self.ops.push({
        'dir': dir,
        'h': h,
      });
    }, 3500);

    int2 = setInterval(function () {
      self.time = parseFloat( (self.time + 0.1).toFixed(2) );

      self.posX -= 10;
      console.log(self.up, window.outerHeight);
      if ((self.up + 185 ) < window.outerHeight){
         self.up += 20;
      }
      document.querySelector('body').style.backgroundPositionX = self.posX + 'px';
      let death = false;
      let myops = document.querySelectorAll('.op');
      for( const i in myops) {
        let my = myops[i];
        if (my.offsetLeft < 350 && my.offsetLeft > 150 ){
          if (my.offsetTop === 0){
            if (my.offsetHeight - 75 > self.up){
              self.health--;
              my.remove();
              break;
            }
          }else{
            if (my.offsetTop < self.up + 40){
              self.health--;
              my.remove();
              break;
            }
          }
        }
      }
      if (self.health == 0){
        clearInterval(int1);
        clearInterval(int2);
        self.ops = [];
      }




    }, 100);
  },
  methods: {
    goUp: function () {
      console.log('goUp');
    },
    rnd: function (min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    }
  }
}
</script>

<style scoped>
  span{
    position: relative;
    z-index: 999;
    padding: 6px;
    font-size: 15px;
  }
  h1{
    font-size: 6em ;
    position: fixed;
    top: 45vh;
    left: 0;
    right: 0;
    text-align: center;
  }
</style>