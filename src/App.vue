<template>
  <div>
    <select v-model="exampleName">
      <option value="composition">Composition</option>
      <option value="options">Options</option>
      <option value="only-template">Only template</option>
    </select>

    <div class="preview">
      <VueLivePreview :code="code" :data-scope="dataScope"/>
    </div>
    <div>
    <VueLiveEditor :code="code" />
  </div>
  </div>

</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { VueLivePreview, VueLiveEditor } from 'vue-live';
import 'prismjs/themes/prism.min.css'
import 'prismjs/themes/prism-funky.min.css'

const code = ref('')
const exampleName = ref('composition')

const dataScope = {
  Date,
}

watch(exampleName, async(name: string) => {
  code.value = await (await fetch(`./${name}.vue`)).text()
}, { immediate: true })

</script>

<style>

.preview {
  border-radius: 8px;
  margin-top: 16px;
  padding: 16px;
  border: 1px solid #ccc;
}
.prism-editor__textarea {
  display: none;
}
.prism-editor__editor {
  text-align: start;
}
</style>