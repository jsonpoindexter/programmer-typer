<template>
  <div id="app">
    <TextBox/>
  </div>
</template>

<script>
  import TextBox from './components/TextBox.vue'

  export default {
  name: 'app',
  components: {
    TextBox
  }
}
</script>

<style>
  html {
    background: grey;
  }

  #app {
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
