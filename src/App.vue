<template>
  <v-calc></v-calc>
</template>

<script>
import vCalc from "@/components/vCalc.vue";

export default {
  name: "App",
  components: {
    vCalc
  }
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
