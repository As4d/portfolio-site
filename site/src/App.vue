<template>
  <div class="app">
    <Boot />
    <Terminal />
  </div>
</template>

<script>
import Boot from "./components/Boot.vue";
import Terminal from "./components/Terminal.vue";

export default {
  components: { Boot, Terminal },
};
</script>

<style>
.app {
  background: black;
  color: #33ff33;
  font-family: "Courier New", monospace;
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column; /* stack boot + terminal */
  overflow: hidden; /* no scrollbars */
  margin: 0;
  padding: 0;
}
</style>
