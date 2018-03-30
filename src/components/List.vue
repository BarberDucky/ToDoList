<template>
  <div id='main'>
    <div id='list'>
      <p v-if="inputs.length === 0"> Add something to do </p>
      <ListInput v-if="criteria(inputs[i-1].checked)"
                 v-for="i in inputs.length"
                 :key="i"
                 :input="inputs[i-1]"
                 @click="update(i-1)"/>
    </div>
    <div id='addBar'>
      <button @click="add()">Add</button>
      <input id='textbox' @keypress.enter="add">
    </div>
    <button @click="showSettings"> Settings </button>
    <div id='settings' style='display: none'>
      <button @click="setCriteria(i-1)"
              v-for="i in criteriaArray.length"
              :key="i" >
              {{ criteriaArray[i-1].text }} </button>
    </div>
  </div>
</template>

<script>
import ListInput from './ListInput.vue'
export default {
  components: {
    ListInput
  },
  data () {
    return {
      inputs: [],
      criteria: (button) => true,
      criteriaArray: [{
        function: (button) => true,
        text: 'Show All'
      },
      {
        function: (button) => button,
        text: 'Show Done'
      },
      {
        function: (button) => !button,
        text: 'Show Not Done'
      }]
    }
  },
  methods: {
    update (i) {
      this.inputs[i].checked = !this.inputs[i].checked
      this.inputs = [...this.inputs]
    },
    add () {
      let textbox = document.getElementById('textbox')
      if (textbox.value !== '') {
        this.inputs.push({
          checked: false,
          text: textbox.value
        })
        this.inputs = [...this.inputs]
        textbox.value = ''
        textbox.focus()
      }
    },
    showSettings () {
      let settings = document.getElementById('settings')
      if (settings.style.display === 'none') {
        settings.style.display = 'flex'
      } else {
        settings.style.display = 'none'
      }
    },
    setCriteria (i) {
      this.criteria = this.criteriaArray[i].function
    }
  }
}
</script>

<style scoped>
    div {
        width: 314px;
        background-color: white;
    }
    #main {
        margin: auto;
        border: 0.5px solid black;
        display: flex;
        flex-direction: column;
    }
    #list {
      display: block;
      overflow-y: scroll;
      height: 435px;
    }
    #addBar {
      display: flex;
      flex-direction: row;
    }
    #settings {
      margin-top: 5px;
      display: none;
      flex-direction: column;
    }
    #settings button {
      margin: 50px;
      margin-top: 10px;
      margin-bottom: 10px;
    }
    p {
      font-size: 40px;
      margin: 60px;
      margin-top: 30px;
    }
    input {
      font-size: 20px;
      flex-grow: 1;
    }
</style>
