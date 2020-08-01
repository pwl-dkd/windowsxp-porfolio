<template>
  <div class="container">
    <Desktop />
    <Windows />
    <Taskbar />
  </div>
</template>

<script>

import Desktop from '../components/Desktop'
import Windows from '../components/Windows'
import Taskbar from '../components/Taskbar'


export default {
  data () {
    return {
      amountApps: 0,
      inactiveWindows: 0,
      allApplications:[
        "Chrome"
      ],
      activeApps: []
    }
  }
}
</script>

<style>

</style>
