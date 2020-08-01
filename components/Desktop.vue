<template>
  <div id="desktop">
    
    <Icon appName="Chrome" Ypos=0 Xpos=0  />



  </div>
</template>

<script>

import Icon from '../components/Icon'


export default {
  name: 'Desktop',
   components: {
    Icon,
  },

}
</script>

<style>
#desktop{
  height:96vh;
  width:100vw;
  background-image: url(~@/assets/images/backgrounds/desktop_wallpaper.jpg);
  background-size: cover ;
}
</style>
