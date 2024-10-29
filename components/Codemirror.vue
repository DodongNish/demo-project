<script setup lang="ts">
import { EditorView, basicSetup } from "codemirror";
import { showMinimap } from "@replit/codemirror-minimap";
import { javascript } from "@codemirror/lang-javascript";
import { oneDark } from "@codemirror/theme-one-dark";

const doc = defineModel<string>();

const codemirrorRef = ref();

// Custom Extensions
const updateDocExtension = EditorView.updateListener.of((view) => {
  if (!view.docChanged) return;
  doc.value = view.state.doc.toString();
});

const showMinimapExtension = showMinimap.compute(["doc"], () => {
  return {
    create: () => ({ dom: document.createElement("div") }),
    displayText: "blocks",
  };
});

const themeExtension = EditorView.theme({
  "&": { height: "400px" },
  // ".cm-scroller": { overflow: "auto" },
  ".cm-minimap-gutter, .cm-minimap-inner > canvas": {
    width: "40px !important",
  },
});

onMounted(() => {
  new EditorView({
    doc: doc.value,
    extensions: [
      themeExtension,
      basicSetup,
      oneDark,
      javascript(),
      updateDocExtension,
      showMinimapExtension,
    ],
    parent: codemirrorRef.value as Element,
  });
});
</script>

<template>
  <div class="w-1/2 h-screen">
    <div ref="codemirrorRef" />
    <!-- <div ref="codemirrorRef" class="h-[400px]" /> -->
  </div>
</template>
