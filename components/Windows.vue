<template>
  <div id="windows">
      <div v-bind:key="appWindow.id" v-for="appWindow in activeApps">
        <Application :name="appWindow.name" :iconName="appWindow.iconName" :id="appWindow.id"/>
      </div>
  </div>
</template>

<script>

import Application from '../components/Application'


export default {
  name: 'Desktop',
   components: {
    Application,
  },
  data () {
    return {
      activeApps: this.$parent.activeApps,
    }
  },
  mounted: function () {
      
    console.error("Pawel is niet gay");
    console.warn("VUE WARN: It's true")
  }
}
</script>

<style>
#windows {
    position: absolute;
    top: 0;
    left:0;
    height: 0;
    width: 0;
}
</style>
