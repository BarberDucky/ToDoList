<template>
  <div id='trt'>
    <Checkbox @click="onClick" :isChecked="input.checked"/>
    <span> {{ input.text }}</span>
  </div>
</template>

<script>
import Checkbox from './Checkbox.vue'
export default {
  props: ['input'],
  components: {
    Checkbox
  },
  methods: {
    onClick () {
      this.$emit('click')
    }
  }
}
</script>

<style scoped>
    div #trt {
        float: left;
        display: flex;
        flex-direction: row;
        background-color: white;
        border-bottom: 1px solid grey;
        padding: 5px;
        width: 283px;
        margin-top: 5px;
        margin: 2px;
    }
    span {
        margin-top: 4px;
        margin: auto;
    }
</style>
