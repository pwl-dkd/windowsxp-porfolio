<template>
  <div class="icon-outer">
    <div class="icon" v-on:click="openApplication" @mousedown="startDragEvent">
      <div class="icon-holder" :style="{'background-image' : 'url(' + require(`@/assets/images/icons/${iconName}.png`) + ')'}">
      </div>
      <p class="icon-name">{{appName}}</p>
    </div>
    <div class="icon ghost" v-if="dragging" :style="{top: current.y - start.y + 'px', left: current.x - start.x + 'px'}">
      <div class="icon-holder" :style="{'background-image' : 'url(' + require(`@/assets/images/icons/${iconName}.png`) + ')'}">
      </div>
      <p class="icon-name">{{appName}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Icon',
  props: [
    'appName', 
    'iconName',
  ],
  data(){
    return{
      dragging: false,
      start: {x: 0, y: 0},
      current: {x: 0,y: 0}
    }
  },
  methods: {
    startDragEvent(e){
      this.start.x = e.pageX;
      this.start.y = e.pageY;
      this.dragging = true;
      this.current.x = e.pageX;
      this.current.y = e.pageY;
      document.addEventListener('mousemove', this.mouseMoveDrag);
    },
    mouseMoveDrag(e){
      this.current.y = e.pageY;
      this.current.x = e.pageX;
    },
    dropEvent(x,y){this.$parent.moveApp(this.appName,x,y);
    },
    openApplication() {

      var activeApps = this.$parent.$parent.activeApps;

      var newWindows =  {
        id: (activeApps.length + 1),  
        name: this.appName,
        iconName: this.iconName
      };

      this.$parent.$parent.inactiveWindows++;

      this.$parent.$parent.activeApps.push(newWindows);

    }
  },
  created: function () {
    let _this = this;
    window.addEventListener('mouseup', (e)=>{
      if(this.dragging){
      this.dropEvent(e.pageX,e.pageY);
      _this.dragging = false;
      document.removeEventListener('mousemove', this.mouseMoveDrag);
      }
    });
  }
}
</script>

<style lang="scss">
.icon-outer{
  height: 100%;
  width: 100%;

}
.icon {
  &.ghost{
    pointer-events: none;
    opacity: .5;
    transform: translateY(-100%);
  }
  height: 100%;
  width: 100%;
  position: relative;
  display: flex;
  flex-direction: column;
  .icon-holder{
    flex: 1;
    margin: 5px;
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
  .icon-name{
    color: white;
    width: 100%;
    text-align: center;
    filter: contrast(1);
    text-shadow: 1px 0px 0px black,0px 1px 0px black,-1px 0px 0px black,0px -1px 0px black;
  }
}
</style>