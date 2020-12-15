<template>
  <div id="app">
    <button @click="debouncedAddButton">Add dynamic button</button>

    <div ref="container" class="button-container"></div>
  </div>
</template>

<script>
import Vue from 'vue'
import Button from './components/Button'
import debounce from 'lodash.debounce'

export default {
  name: 'App',
  data() {
    return {
      buttonIds: [],
      debouncedAddButton: null,
    }
  },
  created() {
    this.debouncedAddButton = debounce(this.addButton, 2000)
  },
  methods: {
    addButton() {
      const ButtonClass = Vue.extend(Button)

      const button = new ButtonClass()
      button.$slots.default = 'Show id'
      button.$mount()

      this.buttonIds.push(button.id)
      this.$refs.container.appendChild(button.$el)
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.button-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 200px;
  margin: 1rem auto;
}

.button-container > button {
  margin-bottom: 0.25rem;
}
</style>
