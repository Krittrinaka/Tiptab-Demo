<template>
  <div id="app">
    <editor-content :editor="editor" />
  </div>
</template>

<script setup>
import { EditorContent, useEditor } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

const editor = useEditor({
  extensions: [StarterKit],
  content: '<p>สวัสดีครับ Hello World!</p>',
})
</script>

<style>
#app {
  max-width: 600px;
  margin: 40px auto;
  font-family: sans-serif;
}
</style>
