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

    <!-- dynamic css -->
    <p>double Clcik on me | Signle click on me</p>
    <div
      class="squar"
      :class="color"
      @dblclick="changeColor"
      @click="changeColorback"
    ></div>
  </div>
</template>

<script>
  export default {
    name: 'Main',
    data() {
      return {
        val: 0,
        color: '',
      }
    },
    methods: {
      plus() {
        return this.val++
      },
      minus() {
        return this.val--
      },
      status() {
        return this.val > 5 ? 'Greater than 5' : 'less than 5'
      },
      changeColor() {
        this.color = 'black'
      },
      changeColorback() {
        this.color = ''
      },
    },
    computed: {
      currentstatus() {
        return this.val > 5 ? 'Greater than 5x' : 'less than 5x'
      },
    },
  }
</script>

<style>
  .squar {
    height: 150px;
    width: 150px;
    background-color: green;
  }

  .black {
    background-color: black;
  }
</style>
