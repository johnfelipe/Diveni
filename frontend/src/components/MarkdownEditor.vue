<template>
  <div class="markdown-editor">
    <viewer v-if="disabled" :initial-value="markdown" :height="height" :options="editorOptions" />
    <editor
      v-else
      ref="toastuiEditor"
      :initial-value="markdown"
      :height="height"
      :options="editorOptions"
      :placeholder="placeholder"
      initial-edit-type="wysiwyg"
      preview-style="vertical"
    />
  </div>
</template>

<script lang="ts">
import "@toast-ui/editor/dist/toastui-editor.css";
import "prismjs/themes/prism.css";
import "@toast-ui/editor-plugin-code-syntax-highlight/dist/toastui-editor-plugin-code-syntax-highlight.css";

import "@toast-ui/editor/dist/i18n/de-de";

import Vue from "vue";
import { Editor, Viewer } from "@toast-ui/vue-editor";
import codeSyntaxHighlight from "@toast-ui/editor-plugin-code-syntax-highlight/dist/toastui-editor-plugin-code-syntax-highlight-all";

export default Vue.extend({
  name: "MarkdownEditor",
  components: {
    editor: Editor,
    viewer: Viewer,
  },
  model: {
    prop: "markdown",
    event: "change",
  },
  props: {
    disabled: {
      type: Boolean,
      default: false,
    },
    height: {
      type: String,
      default: "500px",
    },
    markdown: {
      type: String,
      default: null,
    },
    placeholder: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      editorOptions: {
        autofocus: false,
        height: "auto",
        minHeight: "200px",
        language: this.$i18n.locale,
        useCommandShortcut: true,
        usageStatistics: true,
        hideModeSwitch: false,
        placeholder: this.placeholder,
        extendedAutolinks: true,
        toolbarItems: [
          ["heading", "bold", "italic", "strike"],
          ["hr", "quote"],
          ["ul", "ol", "task", "indent", "outdent"],
          ["table", "image", "link"],
          ["code", "codeblock"],
          ["scrollSync"],
        ],
        plugins: [codeSyntaxHighlight],
      },
    };
  },
});
</script>

<style scoped></style>
