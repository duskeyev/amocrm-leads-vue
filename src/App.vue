<template>
  <div id="app">
    <header>
      <h1>Сделки amoCRM</h1>
    </header>
    <main>
      <Leads />
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Leads from './components/Leads.vue';
export default defineComponent({
  name: 'App',
  components: {
    Leads
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 90%;
  margin-left: 5%;
}
header {
  background: #42b983;
  padding: 20px;
  color: white;

}
main {
  padding: 20px;
}
</style>
