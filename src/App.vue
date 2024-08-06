<template>
  <div id="app">
    <h3>Editable with default</h3>
    <RateBox v-model="rating" :defaultValue="3" />
    <p>Selected Rating: {{ rating }}</p>
    <h3>Editable without default</h3>
    <RateBox v-model="withoutDefaultRating" />
    <p>Selected Rating: {{ withoutDefaultRating }}</p>

    <h3>Not editable</h3>
    <RateBox :modelValue="2" :editable="false" />
    <p>Non-editable Rating: 2</p>
  </div>
</template>

<script setup>
import { ref } from "vue";
import RateBox from "./components/RateBox.vue";

const rating = ref(0);
const withoutDefaultRating = ref(0);
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
</style>
