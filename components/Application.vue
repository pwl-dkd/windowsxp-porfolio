<template>
  <div id="Application" v-on:click="selectedWindow">
      <div v-on:mousedown="dragWindow"  class="windowsHeader">
        <div class="windowName" @mousedown="dragging = true">
          <img class="windowIcon" :src="require( `../assets/images/icons/${name}.png`)" /> 
          <p>{{name}} | {{dragging}}</p>
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
      windowHeight: .45,
      windowWidth: .65,
      windowYPos: .15,
      windowXPos: .17,
    }
  },
  çreated(){
    window.addEventListener('mouseup', ()=>{
      dragging: true,
    });
  },
  methods: {
    OpenApplication() {
      var appWindowData = this.$props
      var appWindow = this.$el;
      var appWindowStyle = appWindow.style;

      appWindowStyle.height = window.innerHeight * this.windowHeight +  'px';
      appWindowStyle.width = window.innerWidth * this.windowWidth +  'px';

      var unselectedWindow = this.$parent.$parent.inactiveWindows * 20 ;

      appWindowStyle.top = window.innerHeight * this.windowYPos + unselectedWindow +  'px';
      appWindowStyle.left = window.innerWidth * this.windowXPos +  unselectedWindow +  'px';
    },
    dragWindow() {
      console.log("mouse is down");
    },
    selectedWindow () {
      if (this.$parent.$parent.inactiveWindows > 0) {
        this.$parent.$parent.inactiveWindows = 0
      }
    }
  },
  mounted: function () {
    this.OpenApplication();
  }
}
</script>

<style>
#Application {
  position:absolute;
  background:red;
  border:1px solid black;
}
.windowsHeader {
  height: 6%;
  width: 100%;
  background:blue;
  background-image: url(~@/assets/images/backgrounds/window_bar.png);
  
}
.windowName {
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
