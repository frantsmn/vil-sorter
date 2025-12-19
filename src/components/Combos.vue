<script setup lang="ts">
import type {VilFile} from "../domain/vil.ts";
import draggable from 'vuedraggable'

const modelValue = defineModel<VilFile['combo']>({required: true, default: []})
</script>

<template>
  <h2>combos</h2>
  <draggable v-model="modelValue">
    <template #item="combo">
      <div class="list-item">
        <div class="list-item__index">{{ combo.index + 1 }}</div>
        <span class="key" v-for="key in combo.element">{{ key }}</span>
      </div>
    </template>
  </draggable>
</template>

<style scoped>
.list-item  {
  background: rgba(127, 255, 212, 0.15);
  border-radius: 5px;
  display: flex;
  gap: 1rem;
  padding: .2rem .4rem;
  margin-block: .2rem 0;
  align-items: center;

  .list-item__index{
    opacity: .4;
  }
}

.key {
  border: rgba(255, 255, 255, 0.4) 1px solid;
  padding: .4rem;
  border-radius: 5px;
}
</style>