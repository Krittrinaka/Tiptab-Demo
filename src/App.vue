<template>
  <div class="editor-container">
    <div class="toolbar">
      <button @click="toggleBold">Bold</button>
      <button @click="toggleItalic">Italic</button>
      <button @click="toggleUnderline">Underline</button>
      <button @click="exportHTML">Export HTML</button>
      <button @click="exportJSON">Export JSON</button>
      <button @click="toggleLanguage">{{ currentLanguage }}</button>
    </div>
    <EditorContent :editor="editor" />
    <div class="output">
      <h3>Exported Content</h3>
      <pre>{{ exportedContent }}</pre>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { EditorContent, useEditor } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import Underline from '@tiptap/extension-underline'
import Placeholder from '@tiptap/extension-placeholder'

const currentLanguage = ref('ไทย')
const exportedContent = ref('')

const editor = useEditor({
  extensions: [
    StarterKit,
    Underline,
    Placeholder.configure({
      placeholder: 'พิมพ์ข้อความที่นี่ / Type your content here...',
    }),
  ],
  content: '',
})

const toggleBold = () => editor.chain().focus().toggleBold().run()
const toggleItalic = () => editor.chain().focus().toggleItalic().run()
const toggleUnderline = () => editor.chain().focus().toggleUnderline().run()
const exportHTML = () => exportedContent.value = editor.getHTML()
const exportJSON = () => exportedContent.value = JSON.stringify(editor.getJSON(), null, 2)
const toggleLanguage = () => {
  currentLanguage.value = currentLanguage.value === 'ไทย' ? 'English' : 'ไทย'
}
</script>

<style>
.editor-container {
  max-width: 800px;
  margin: auto;
  padding: 20px;
}
.toolbar {
  margin-bottom: 10px;
}
.toolbar button {
  margin-right: 5px;
}
.output {
  margin-top: 20px;
  background: #f0f0f0;
  padding: 10px;
}
</style>
