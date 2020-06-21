<template>
  <div class="container">
    <h2>Vue Componets</h2>
    <button @click="plus">Increase</button>
    <button @click="minus">Decrease</button>
    <p>{{ val }}</p>
    <!-- this function will call everytime No matter the data property update or not  -->
    <p>{{ status() }}</p>
    <!-- this will call the computed property which will only update accoding to the data  -->
    <p>{{ currentstatus }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Main',
    data() {
      return {
        val: 0,
      }
    },
    methods: {
      plus() {
        return this.val++
      },
      minus() {
        return this.val--
      },
      plus2x() {
        return (this.val = this.val * 2)
      },
      status() {
        return this.val > 5 ? 'Greater than 5' : 'less than 5'
      },
    },
    computed: {
      currentstatus() {
        return this.val > 5 ? 'Greater than 5x' : 'less than 5x'
      },
    },
  }
</script>

<style></style>
