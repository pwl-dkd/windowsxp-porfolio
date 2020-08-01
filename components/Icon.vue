<template>
  <div id="icon" v-on:click="openApplication" >
    <p>dit is {{appName}}</p>
    <p>( {{Xpos}} , {{Ypos}} )</p>
  </div>

</template>

<script>
export default {
  name: 'Icon',
  props: [
    'appName', 
    'Ypos',
    'Xpos'
  ],
  methods: {
    bootIcon() {
      var iconData = this.$props
      var icon = this.$el;
      var iconStyle = icon.style;

      var iconHeight = (window.innerHeight * 0.096 );
      var iconWidth = (window.innerWidth / 15 );

      iconStyle.top = (iconHeight * iconData.Ypos) / window.innerHeight * 100 + '%' ;
      iconStyle.left = (iconWidth * iconData.Xpos) / window.innerWidth * 100 + '%' ;

    },
    openApplication() {

      var activeApps = this.$parent.$parent.activeApps;

      var newWindows =  {
        id: (activeApps.length + 1),
          name:this.appName
      };

      this.$parent.$parent.inactiveWindows++;

      this.$parent.$parent.activeApps.push(newWindows);

    }
  },
  mounted: function () {
    this.bootIcon();
  }
  
}
</script>

<style>
#icon {
  width: calc(100vw / 15);
  height: calc(96vh / 10);
  position: absolute;
  background-color:red;
}
</style>
