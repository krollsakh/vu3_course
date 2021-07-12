<template>
  <button class="btn">
    <slot></slot>
  </button>

</template>

<script>
export default {
  name: 'my-button'
}
</script>

<style scoped>
.btn {
  padding: 10px;
  background: none;
  border: 1px solid #0279F0FF;
}
</style>
