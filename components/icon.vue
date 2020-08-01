<template>
  <div class="icon">
    <div></div>
    <span>
      {{ name }}
      <br />
      [{{ posX }}|{{ posY }}]
    </span>
  </div>
</template>

<script>
export default {
  name: 'icon',
  props: {
    posX: String,
    posY: String,
    name: String,
    iconUrl: String
  }
}
</script>

<style lang="scss">
.icon {
  height: 150px;
  width: 150px;
  display: flex;
  text-align: center;
  flex-direction: column;
  > div {
    flex: 1;
    background-image: radial-gradient(
      circle at center,
      blue 50%,
      transparent 51%
    );
  }
  > span {
    color: white;
    filter: contrast(1);
    text-shadow: 0px -1px 0 black, 1px 0px 0 black, -1px 0px 0 black,
      0px 1px 0 black, -0.5px -0.5px 0 black, 0.5px -0.5px 0 black,
      -0.5px 0.5px 0 black, 0.5px 0.5px 0 black;
    flex: 0;
  }
}
</style>
