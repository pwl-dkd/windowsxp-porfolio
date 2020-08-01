<template>
  <div id="Application" :class="{'dragging': dragging}" class="app" v-on:click="selectedWindow" :style="{'width': windowWidth + 'px','height': windowHeight + 'px','top': windowYPos + 'px','left': windowXPos + 'px'}">
      <div class="windowsHeader">
        <div class="windowName" @mousedown="dragEvent">
          <img class="windowIcon" :src="require( `../assets/images/icons/${name}.png`)" /> 
          <p>{{name}}</p>
        </div>
      </div>
  </div>
</template>

<script>


export default {
  name: 'Application',
   props: [
    'id', 
    'name'
  ],
  data () {
    return {
      dragging: false,
      windowHeight: 100,
      windowWidth: 100,
      windowYPos: 100,
      windowXPos: 100,
    }
  },
  created(){
    let _this = this;
    window.addEventListener('mouseup', ()=>{
      _this.dragging = false;
      document.removeEventListener('mousemove', this.mouseMoveDrag);
    });

    this.windowYPos = window.innerHeight * 0.1;
    this.windowXPos = window.innerWidth * 0.1;
    this.windowWidth = window.innerWidth * 0.8;
    this.windowHeight = window.innerHeight * 0.8;


    let windowsPositions = [];
    let windows = document.body.querySelectorAll("#windows div div.app");
    
    console.log(windowsPositions);

    //window placement logic here;
  },
  methods: {
    dragEvent(e){
      this.dragging = true;
      document.addEventListener('mousemove', this.mouseMoveDrag);
    },
    mouseMoveDrag(e){
      this.windowYPos += e.movementY;
      this.windowXPos += e.movementX;
    },
    selectedWindow () {
      if (this.$parent.$parent.inactiveWindows > 0) {
        this.$parent.$parent.inactiveWindows = 0
      }
    }
  },
}
</script>

<style>
.app {
  position:absolute;
  background:red;
  border:1px solid black;
}
.dragging{
  opacity: .75;
}
.windowsHeader {
  height: 28px;
  width: 100%;
  background:blue;
  background-position: center;
  background-size: auto 100%;
  background-image: url(~@/assets/images/backgrounds/window_bar.png);
  
}
.windowName {
  height: 100%;
  font-size: 12px;
  text-shadow: 1px 1px 1px #000;
  color:white;
  font-weight: bold;
  line-height: 161%;
  padding: 0.2%;
}

.windowName * {
    display: inline-block;
}

.windowIcon {
  width:1.2%;
  vertical-align: sub;
}
</style>
