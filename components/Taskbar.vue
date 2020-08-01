<template>
  <div id="taskbar">
    <div id="active apps"></div>
  </div>
</template>

<script>
export default {
  name: 'Taskbar',
  mounted: function () {
    console.log('mounted');
  }
}
</script>

<style>
#taskbar{
  /* background-color:red; */
  width: 100%;
  height:4vh;

  background-size: auto 100%;

  background-image: url(~@/assets/images/backgrounds/window_bar.png);
}
</style>
