<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div @click.stop class="dialog__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'my-dialog',
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideDialog () {
      console.log('click')
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
.dialog {
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  position: fixed;
  background: rgba(0, 0, 0, 0.25);
}

.dialog__content {
  padding: 10px;
  margin: auto;
  border-radius: 8px;
  background: #fff;
  width: 400px;
  /*height: available;*/
}
</style>
