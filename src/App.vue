<template>
  <Salaries />
</template>

<script>
import SalariesVue from "./components/Salaries.vue";
export default {
  name: "App",
  components: {
    Salaries: SalariesVue,
  },
};
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
