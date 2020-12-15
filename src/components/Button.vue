<template>
  <button @click="showId">
    <slot />
  </button>
</template>

<script>
export default {
  name: 'Button',
  data() {
    return {
      id: null
    }
  },
  created() {
    this.id = this._uid
  },
  methods: {
    showId() {
      alert(this.id)
    }
  }
}
</script>

<style scoped>

</style>
