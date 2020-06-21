<template>
  <div class="container">
    <h3>Conditions and lists in vue</h3>
    <div v-if="show">
      Pikabooooo
    </div>
    <!-- v-show just hide or show the content in the display -->
    <div v-show="vshow">
      Pikabooooo
    </div>
    <br />
    <button @click="show = !show">v If Else</button>
    <button @click="vshow = !vshow">v Show</button>
  </div>
</template>

<script>
  export default {
    name: 'ConditionsList',
    data() {
      return {
        x: null,
        show: false,
        vshow: false,
      }
    },
  }
</script>

<style></style>
