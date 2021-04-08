<template>
  <div class="editor-container">
    <div v-if="editor" class="icons">
      <BoldIcon name="ri-bold" :class="{ 'is-active': editor.isActive('bold') }" @click="editor.chain().focus().toggleBold().run()" />
      <ItalicIcon :class="{ 'is-active': editor.isActive('italic') }" @click="editor.chain().focus().toggleItalic().run()" />
      <StrikeIcon :class="{ 'is-active': editor.isActive('strike') }" @click="editor.chain().focus().toggleStrike().run()" />
      <CodeIcon :class="{ 'is-active': editor.isActive('code') }" @click="editor.chain().focus().toggleCode().run()" />
      <ParagraphIcon :class="{ 'is-active': editor.isActive('paragraph') }" @click="editor.chain().focus().setParagraph().run()" />
      <H1Icon :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }" @click="editor.chain().focus().toggleHeading({ level: 1 }).run()" />
      <H2Icon :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }" @click="editor.chain().focus().toggleHeading({ level: 2 }).run()" />
      <H3Icon :class="{ 'is-active': editor.isActive('heading', { level: 3 }) }" @click="editor.chain().focus().toggleHeading({ level: 3 }).run()" />
      <H4Icon :class="{ 'is-active': editor.isActive('heading', { level: 4 }) }" @click="editor.chain().focus().toggleHeading({ level: 4 }).run()" />
      <H5Icon :class="{ 'is-active': editor.isActive('heading', { level: 5 }) }" @click="editor.chain().focus().toggleHeading({ level: 5 }).run()" />
      <H6Icon :class="{ 'is-active': editor.isActive('heading', { level: 6 }) }" @click="editor.chain().focus().toggleHeading({ level: 6 }).run()" />
      <ListUnorderedIcon :class="{ 'is-active': editor.isActive('bulletList') }" @click="editor.chain().focus().toggleBulletList().run()" />
      <ListOrderedIcon :class="{ 'is-active': editor.isActive('orderedList') }" @click="editor.chain().focus().toggleOrderedList().run()" />
      <QuotesIcon :class="{ 'is-active': editor.isActive('blockquote') }" @click="editor.chain().focus().toggleBlockquote().run()" />
      <SeparatorIcon @click="editor.chain().focus().setHorizontalRule().run()" />
      <UndoIcon @click="editor.chain().focus().undo().run()" />
      <RedoIcon @click="editor.chain().focus().redo().run()" />
    </div>
    <editor-content :editor="editor" :v-model="content" />
  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-2'
import { defaultExtensions } from '@tiptap/starter-kit'
import BoldIcon from '@/assets/icons/bold.svg?inline'
import ItalicIcon from '@/assets/icons/italic.svg?inline'
import StrikeIcon from '@/assets/icons/strikethrough.svg?inline'
import CodeIcon from '@/assets/icons/code-view.svg?inline'
import ParagraphIcon from '@/assets/icons/paragraph.svg?inline'
import H1Icon from '@/assets/icons/h-1.svg?inline'
import H2Icon from '@/assets/icons/h-2.svg?inline'
import H3Icon from '@/assets/icons/h-3.svg?inline'
import H4Icon from '@/assets/icons/h-4.svg?inline'
import H5Icon from '@/assets/icons/h-5.svg?inline'
import H6Icon from '@/assets/icons/h-6.svg?inline'
import ListOrderedIcon from '@/assets/icons/list-ordered.svg?inline'
import ListUnorderedIcon from '@/assets/icons/list-unordered.svg?inline'
import QuotesIcon from '@/assets/icons/double-quotes-l.svg?inline'
import SeparatorIcon from '@/assets/icons/separator.svg?inline'
import UndoIcon from '@/assets/icons/arrow-go-back-line.svg?inline'
import RedoIcon from '@/assets/icons/arrow-go-forward-line.svg?inline'

export default {
  components: {
    EditorContent,
    BoldIcon,
    ItalicIcon,
    StrikeIcon,
    CodeIcon,
    ParagraphIcon,
    H1Icon,
    H2Icon,
    H3Icon,
    H4Icon,
    H5Icon,
    H6Icon,
    ListOrderedIcon,
    ListUnorderedIcon,
    QuotesIcon,
    SeparatorIcon,
    UndoIcon,
    RedoIcon
  },

  data () {
    return {
      editor: null,
      content: ''
    }
  },

  mounted () {
    this.editor = new Editor({
      content: '<p>I’m running tiptap with Vue.js. 🎉</p>',
      extensions: defaultExtensions()
    })
  },

  beforeDestroy () {
    this.editor.destroy()
  }
}
</script>

<style scoped lang="sass">
.editor-container
  padding: $m
  background: $white
  border-radius: 8px
  border: 1px solid $ui5

  div
    .ProseMirror.ProseMirror-focused
      outline: 0px solid black

.icons
  margin-bottom: $l
  svg
    height: 20px
    width: 20px
    fill: $ui3
    margin-right: $s
    cursor: pointer

    &:hover
      fill: $ui1

    &.is-active
      fill: $primary

</style>
