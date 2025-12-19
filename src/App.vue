<script setup lang="ts">
import {ref} from 'vue'
import type {VilFile} from './domain/vil.ts'
import AsidePanel from './components/AsidePanel.vue'
import Combos from './components/Combos.vue'

const vil = ref<VilFile>({})
</script>

<template>
    <AsidePanel v-model="vil"/>
  <main>
    <Combos v-model="vil.combo"/>
  </main>
</template>
