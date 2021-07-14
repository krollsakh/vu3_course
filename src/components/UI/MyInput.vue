<template>
  <input class="input" :value="modelValue" @input="onInput" type="text">
</template>

<script>
export default {
  name: 'my-input',
  props: {
    modelValue: {
      type: [String, Number]
    }
  },
  methods: {
    onInput (event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>
input {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #0279F0FF;
  box-shadow: none;

}

</style>
