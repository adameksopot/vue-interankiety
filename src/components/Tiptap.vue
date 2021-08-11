<template>
  <div>
    <div v-if="editor">
      
      <button @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
        <i class="ri-bold"></i> 
      </button>
      <button @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
      <i class="ri-italic"></i> 
      </button>
      <button @click="editor.chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
         <i class="ri-strikethrough"></i> 
      </button>
        <button @click="editor.chain().focus().toggleUnderline().run()" :class="{ 'is-active': editor.isActive('underline') }">
       <i class="ri-underline"></i> 
    </button>
     <button @click="setLink" :class="{ 'is-active': editor.isActive('link') }">
      <i class="ri-link"></i>
    </button>
 
    </div>
    <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import Link from '@tiptap/extension-link'
import Underline from '@tiptap/extension-underline'
export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      editor: null,
    }
  },

  mounted() {
    this.editor = new Editor({
      extensions: [
        StarterKit,
        Link,
        Underline
      ],
      content: `
       text here...
      `,
    })
  },

   methods: {
    setLink() {
      const url = window.prompt('URL')

      this.editor
        .chain()
        .focus()
        .extendMarkRange('link')
        .setLink({ href: url })
        .run()
    },
  },

  beforeUnmount() {
    this.editor.destroy()
  },
}
</script>

