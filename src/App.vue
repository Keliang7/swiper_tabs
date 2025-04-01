<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import PageView from "./components/PageView/pageview.vue";
</script>

<template>
  <div>
    <PageView :headerBgColor="'yellow'">
      <HelloWorld msg="Vite + Vue" />
    </PageView>
  </div>
</template>
