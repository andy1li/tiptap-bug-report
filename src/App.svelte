<script lang="ts">
  import { onMount } from 'svelte'
  import { Editor } from '@tiptap/core'
  import Document from '@tiptap/extension-document'
  import Paragraph from '@tiptap/extension-paragraph'
  import Text from '@tiptap/extension-text'

  let editor: Editor, element: HTMLElement

  onMount(() => {
    editor = new Editor({
      element,
      extensions: [Document, Paragraph, Text],
      content: '123',
      onTransaction: () => (editor = editor),
      onUpdate: ({ editor }) => {null},
    })
    return () => editor?.destroy()
  })
</script>

<div 
  bind:this={element}
/>

{editor && editor.getHTML()}