<template>
  <div class="world">
    <audio ref="musicPlayer" autoplay loop>
      <source src="../soundtrack/music.mp3" type="audio/mpeg">
    </audio>
    <div v-if="!welcomeMsg" class="banner">
       <h1 class="banner__title">Super Luigi</h1>
       <!--<h1 v-if="welcomeMsg" class="banner__title">Comming soon</h1>-->
     </div>
     <a v-if="!welcomeMsg" @click="startFunc" class="button button-start" href="#">Start</a>
     <MarioCharacter :start="startValue" />
     <div v-if="welcomeMsg" class="obstacles">
       <div class="obstacles__item"></div>
       <div class="obstacles__item"></div>
       <div class="obstacles__item"></div>
     </div>
     <div class="land"></div>
  </div>
</template>

<script>
import MarioCharacter from './MarioCharacter.vue'
export default {
  name: 'HelloWorld',
  components: {
    MarioCharacter
  },
  data() {
    return {
      startValue: false,
      welcomeMsg: false,
    }
  },
  methods: {
    startFunc(e) {
      e.preventDefault();
      this.startValue = true;
      //this.$refs.musicPlayer.play();
      setTimeout(() => {
        this.welcomeMsg = true;
      }, 4000);
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.button {
  text-decoration: none;
  background-color: #9a6e32;
  color: #fff;
  transition: all .25s cubic-bezier(.25,.46,.45,.94);
  border-radius: 8px;
  text-transform: uppercase;
  text-align: center;
}

.button:hover {
  background-color:#c89856;
  transition: all .25s cubic-bezier(.25,.46,.45,.94);
}

.button-start {
  padding: 10px 20px;
  position: absolute;
  top: 324px;
  left: 0;
  right: 0;
  max-width: 60px;
  margin: 0 auto;
}

.world {
  overflow: hidden;
  position: relative;
  background-image: url('../images/sky.png');
  background-repeat: no-repeat;
  background-size: cover;
  height: 100vh;
  width: 100vw;
}

.land {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 116px;
  background-image: url('../images/land.jpg');
}

.banner {
  position: absolute;
  top: 80px;
  left: 0;
  right: 0;
  max-width: 416px;
  margin: 0 auto;
  background-color: #e35909;
  -webkit-box-shadow: -4px 6px 17px 6px rgba(0,0,0,0.26); 
  box-shadow: -4px 6px 17px 6px rgba(0,0,0,0.26);
}

.banner:after {
  content: '';
  display: block;
  position: absolute;
  top: -4px;
  left: -2px;
  width: 99%;
  height: 98%;
  background: transparent;
  border: 6px solid transparent;
  animation: circular-border 1s linear infinite;
}

.banner__title {
  margin: 0;
  padding: 60px 30px;
  color: #fff;
  font-size: 60px;
}

.obstacles {
  position: absolute;
  top: 70%;
  right: -10%;
  width: 100%;
}

.obstacles__item {
  position: relative;
  display: inline-block;
  width: 80px;
  height: 70px;
  background-color: #42b983;
  margin-right: 15%;
}

.obstacles__item::before {
  content: '';
  position: absolute;
  display: block;
  width: 100px;
  height: 20px;
  background-color: #42b983;
  left: -10px;
}

@keyframes circular-border {
    0% {
      border-color: #e35909;
    }
 
    50% {
      border-color: #fffb26;
    }
 
    100% {
      border-color: #e35909;
    }
}
</style>
