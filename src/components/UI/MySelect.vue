<template>
  <select v-model="modelValue" @change="changeOptions">
    <option disabled value="">Выберите сортировку</option>
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
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
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

</style>
