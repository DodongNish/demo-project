<script setup lang="ts">
import { EditorView, basicSetup } from "codemirror";
import { showMinimap } from "@replit/codemirror-minimap";
import { javascript } from "@codemirror/lang-javascript";
import { oneDark } from "@codemirror/theme-one-dark";

const codemirrorRef = ref();

const create = () => {
  const dom = document.createElement("div");
  return { dom };
};

onMounted(() => {
  new EditorView({
    doc: "",
    extensions: [
      basicSetup,
      oneDark,
      javascript(),
      showMinimap.compute(["doc"], () => {
        return {
          create,
          /* optional */
          displayText: "blocks",
        };
      }),
      EditorView.theme({
        "&": { height: "300px" },
        ".cm-minimap-gutter, .cm-minimap-inner > canvas": {
          width: "40px !important",
        },
      }),
    ],

    parent: codemirrorRef.value as Element,
  });
});
</script>

<template>
  <div ref="codemirrorRef" class="h-screen" />
</template>
