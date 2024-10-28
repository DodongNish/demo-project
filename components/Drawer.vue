<script setup lang="ts">
const items = [
  {
    title: "Timer",
    value: "timer",
    children: { icon: "mdi-timer", path: "/timer" },
  },
  {
    title: "Code Editor",
    value: "code-editor",
    children: { icon: "mdi-code-braces", path: "/code-editor" },
  },
];
</script>

<template>
  <v-navigation-drawer expand-on-hover rail>
    <v-list>
      <v-list-item
        prepend-avatar="/public/title-img.jpg"
        subtitle="Dodong Nish"
        title="Ryuichi Nishimura"
      ></v-list-item>
    </v-list>

    <v-divider />

    <v-list density="compact" nav>
      <v-list-item
        v-for="item in items"
        :key="item.title"
        link
        @click="navigateTo(item.children.path)"
        :title="item.title"
        :prepend-icon="item.children.icon"
        :value="item.title"
      >
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>
