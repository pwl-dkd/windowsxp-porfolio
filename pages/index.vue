<template>
  <div id="main">
    <desktop></desktop>
    <navbar></navbar>
  </div>
</template>

<script>
import desktop from '~/components/desktop.vue'
import navbar from '~/components/navbar.vue'

export default {
  components: {
    desktop,
    navbar
  }
}
</script>

<style lang="scss">
#main {
  width: 100vw;
  position: fixed;
  height: 100vh;
  display: flex;
  flex-direction: column;
  font-family: tahoma, sans-serif;
  #desktop {
    background-image: url(~@/assets/background/background.jpg);
    background-size: cover;
    background-position: center;
    flex: 1;
  }
  #navbar {
    background-color: #245edc;
    background-image: linear-gradient(
      to bottom,
      #4993e6,
      transparent 12px,
      transparent calc(100% - 12px),
      #1941a5
    );
    flex: 0 0 30px;
  }
}
</style>
