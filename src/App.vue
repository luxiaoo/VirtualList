<template>
  <div id="app">
    <HelloWorld :listData = "data" :itemSize ="100"/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
let d = [];
for (let i = 0; i < 1000; i++) {
  d.push({ id: i, value: i });
}

export default {
  name: "app",
  components: {
    HelloWorld
  },
  data() {
    return {data: d};
  }
};
</script>

<style>
html {
  height: 100%;
}
body {
  height: 100%;
  margin: 0;
}
#app {
  height: 100%;
}
</style>
