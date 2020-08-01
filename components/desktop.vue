<template>
  <div id="desktop">
    <DesktopIcon
      pos-x="2"
      pos-y="4"
      name="Microsoft Edge"
      icon-url="/"
    ></DesktopIcon>
  </div>
</template>

<script>
import DesktopIcon from '~/components/icon.vue'

export default {
  name: 'Desktop',
  components: { DesktopIcon }
}
</script>

<style lang="scss">
#desktop {
  display: flex;
}
</style>
