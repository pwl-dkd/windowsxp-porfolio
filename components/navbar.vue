<template>
  <div id="navbar">
    <div id="navStart">start</div>
    <div class="appSpace"></div>
    <div id="navTime">12:00<br />1-04-2000</div>
  </div>
</template>

<script>
export default {
  name: 'navbar',
  data() {
    return {
      date: new Date()
    }
  }
}
</script>

<style lang="scss">
#navbar {
  display: flex;

  #navStart {
    background: green;
    flex: 0 0 6vw;
    height: 100%;
  }
  .appSpace {
    flex: 1;
  }
  #navTime {
    flex: 0 0 8vw;
    text-align: center;
    height: 100%;
    align-self: flex-end;
  }
}
</style>
