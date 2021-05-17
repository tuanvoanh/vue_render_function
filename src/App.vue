<template>
  <div>
    <h2>Demo Vue Render Function v2.0</h2>
    <Heading :level="1">TV Finder</Heading>
    <MyShow />
  </div>
</template>

<script setup>
import Heading from "./components/Heading.vue";
import MyShow from "./components/MyShow.vue";
import HelloWorld from "./components/HelloWorld.vue";
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>

<style>
#app {
  text-align: center;
}
</style>
