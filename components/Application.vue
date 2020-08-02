<template>
  <div id="Application" :class="{'dragging': dragging, 'fullscreen': fullscreen}" class="app" v-on:click="selectedWindow" :style="{'width': windowWidth + 'px','height': windowHeight + 'px','top': windowYPos + 'px','left': windowXPos + 'px'}">
      <div class="windowsHeader">
        <div class="windowName" @mousedown="dragEvent">
          <img class="windowIcon" :src="require( `../assets/images/icons/${iconName}.png`)" /> 
          <p>{{name}}</p>
          <button @click="fullScreenWindow" >
             <i v-if="!fullscreen">Full</i><i v-else>Mini</i>
            </button>
          <p @click="closeWindow" >close</p>
        </div>
      </div>
  </div>
</template>

<script>


export default {
  name: 'Application',
   props: [
    'id', 
    'name',
    'iconName'
  ],
  data () {
    return {
      dragging: false,
      fullscreen: false,
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

    this.windowYPos = Math.round(window.innerHeight * 0.1);
    this.windowXPos = Math.round(window.innerWidth * 0.1);
    this.windowWidth = Math.round(window.innerWidth * 0.8);
    this.windowHeight = Math.round(window.innerHeight * 0.8);


    let windowsPositions = [];
    let windows = document.body.querySelectorAll("#windows div div.app");
    
    for (let i = 0; i < windows.length; i++){
      windowsPositions.push({
        x: parseInt(windows[i].style.left),
        y: parseInt(windows[i].style.top)
      })
    }
    //window placement logic here;
    while (windowsPositions.findIndex(wp => wp.x === _this.windowXPos && wp.y === _this.windowYPos) !== -1){
      this.windowYPos += 20;
      this.windowXPos += 20;
      if (this.windowYPos > window.innerHeight - 20){
        this.windowYPos = 0;
      }
      if (this.windowXPos > window.innerWidth - 20){
        this.windowXPos = 0;
      }
    }
    
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
    },
    closeWindow(){
      console.log(this);
      let activeWindows = this.$parent.$parent.activeApps;  
  	  let currentApplication = this.id;
      let appId = currentApplication - 1;

      for(let i = 0; i < this.$parent.$parent.activeApps.length; i++) {
        if (activeWindows[i].id == 1) 
          this.$parent.$parent.activeApps.splice(appId, 1);
      }
    },
    fullScreenWindow () {
      this.fullscreen = !this.fullscreen;
    }
  },
}
</script>

<style lang="scss">
.app {
  position:absolute;
  background:red;
  border:1px solid black;
  &.fullscreen{
    height: calc(100vh - 4vh) !important;
    width: 100vw !important;
    top:0 !important;
    left:0 !important;
  }
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
