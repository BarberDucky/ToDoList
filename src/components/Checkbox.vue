<template>
  <div @click="onClick">
      <img v-if="isChecked" ref='img' src='../assets/checked.png' />
  </div>
</template>

<script>
export default {
  props: ['isChecked'],
  data () {
    return {
    }
  },
  methods: {
    onClick () {
      this.$emit('check')
    }
  }
}
</script>

<style scoped>
    div {
        border: 2px solid skyblue;
        border-radius: 5px;
        height: 20px;
        width: 20px;
    }
    img {
        max-width: 100%;
        max-height: 100%;
    }
</style>
