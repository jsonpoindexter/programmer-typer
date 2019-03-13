<template>
  <textarea class='text-input'></textarea>
</template>

<script>
export default {
  name: 'TextBox',
  props: {
    msg: String
  }
}
</script>

<style scoped>

  .text-input {
    height: 500px;
    width: 600px;
    background: grey;
    border: none;
  }
</style>
