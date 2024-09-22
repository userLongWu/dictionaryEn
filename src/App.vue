<script setup lang="ts">
import Header from './components/Header.vue'
import Definiton from './components/Definiton.vue'
import { ref } from "vue";
const searchWord = ref();
</script>

<template>
<div class="container">
    <main>
      <Header v-model="searchWord" />
      <Definiton :searchWord='searchWord'/>
    </main>
  </div>
</template>

<style lang="less" scoped>
div.container {
  height: 100vh;
  overflow: hidden;
  background-color: #282c34;
  main {
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    color: white;
    padding: 1rem;
  }
}
</style>
