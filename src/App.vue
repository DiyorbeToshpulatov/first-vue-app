<template>
  <Navbar />
  <RouterView></RouterView>
</template>

<script setup>
import Navbar from './components/Navbar.vue';
import { RouterView } from 'vue-router';

components: {
  Navbar;
}
</script>
