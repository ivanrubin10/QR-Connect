<script setup lang="ts">
import QRApp from '../components/QRApp.vue'
import AppHeader from  '../components/AppHeader.vue'
</script>

<template>
  <main>
    <AppHeader>
      <template #title>
        <h1>QR Connect</h1>
      </template>
    </AppHeader>
    <QRApp />
  </main>
</template>

<style scoped>
main {
  height: 100%;
}
h1 {
  margin: 0px;
}
</style>