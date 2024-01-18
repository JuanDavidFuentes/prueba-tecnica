<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="glossy">
      <q-toolbar>
        <!-- <q-btn flat dense round @click="leftDrawerOpen = !leftDrawerOpen" aria-label="Menu" icon="menu" /> -->

        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    

    <q-page-container>
      <HelloWorld />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const leftDrawerOpen = ref(false)


</script>
