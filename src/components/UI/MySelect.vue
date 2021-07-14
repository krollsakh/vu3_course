<template>
  <select
    :value="modelValue"
    @change="changeOptions"
  >
    <option disabled value="">Выберите значение из списка</option>
    <option
      v-for="option in options"
      :key="option.value"
      :value="option.value"
    >
      {{ option.title }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'my-select',
  props: {
    options: {
      type: Array,
      default: () => []
    },
    modelValue: {
      type: String
    }
  },
  methods: {
    changeOptions (e) {
      this.$emit('update:modelValue', e.target.value)
    }
  }
}
</script>

<style scoped>

select {
  border: 1px solid #0279F0FF;
  padding: 10px;
}

:focus {
  box-shadow: 0 0 5px 0 #0279F0FF;
}
</style>
