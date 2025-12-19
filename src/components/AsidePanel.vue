<script setup lang="ts">
import {computed, ref, useTemplateRef} from 'vue'
import type {VilFile} from '../domain/vil.ts'

const modelValue = defineModel<VilFile>({required: true})

const fileInput = useTemplateRef('fileInput')
const vilFileContent = ref('')

const onFileChange = async () => {
  const file = fileInput?.value?.files?.[0];
  if (!file) return

  vilFileContent.value = await file.text()
  modelValue.value = JSON.parse(vilFileContent.value)
}

const modelValueStr = computed({
  get: () => JSON.stringify(modelValue.value),
  set: (value: string) => {
    modelValue.value = JSON.parse(value)
  }
})

const downloadVil = () => {
  const json = JSON.stringify(modelValue.value, null, 2);

  const blob = new Blob([json], {
    type: 'application/json',
  });

  const url = URL.createObjectURL(blob);

  const a = document.createElement('a');
  a.href = url;
  a.download = 'keymap.vil';
  a.click();

  URL.revokeObjectURL(url);
}
</script>

<template>
  <aside>
    <h1>vil sorter</h1>
    <input ref="fileInput" @change="onFileChange" type="file"/>
    <br>
    <textarea v-model="modelValueStr"></textarea>
    <br>
    <a href="#" @click.prevent="downloadVil">download</a>
  </aside>
</template>
