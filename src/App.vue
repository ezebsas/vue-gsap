<template>
  <div id='app' class="App">
    <header class="App-header">
      <div class="circle-container">
        <div ref='circle' class="circle"></div>
        <div ref='circleRed' @click='handleExpand' class="circle red"></div>
        <div ref='circleBlue' class="circle blue"></div>
      </div>
    </header>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  name: 'App',
  data(){
    return {
      state: false,
      circle: null,
      circleRed: null,
      circleBlue: null,
    }
  },
  methods: {
    handleExpand: function(){
      if (!this.state) {
        gsap.to(this.circleRed,
          {
            duration: .8,
            width:200,
            height: 200,
            ease: 'power.in'
          }
        )
        this.state = true;
      }
      else{
        gsap.to(this.circleRed,
          {
            duration: .8,
            width:75,
            height: 75,
            ease: 'power.in'
          }
        )
        this.state = false
      }
    },
  },
  components: {
  },
  mounted: function(){
    this.circle = this.$refs.circle
    this.circleRed = this.$refs.circleRed
    this.circleBlue = this.$refs.circleBlue
    gsap.to('.App', {duration:0, css: {visibility: 'visible'}})
    gsap.from([this.circle, this.circleRed, this.circleBlue], {
      duration: .8,
      opacity:0,
      x: 40,
      ease: 'power3.in',
      stagger: .2
    })
  },
}
</script>

<style>
.App {
  text-align: center;
  visibility: hidden;
}

.App-header {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.circle{
  width: 75px;
  height: 75px;
  border-radius: 100%;
  background-color: #fdcf51;
  margin: 50px;
}

.circle.red{
  background-color: #fd5151;
}

.circle.blue{
  background-color: #51a0fd;
}
</style>
