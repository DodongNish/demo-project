<script setup lang="ts">
const isCountingUp = ref(false);
const time = ref(0);
const intervalId = ref();

const start = () => {
  if (intervalId.value != null) return;
  isCountingUp.value = true;
  countUp();
};
const stop = () => {
  isCountingUp.value = false;
  clearInterval(intervalId.value);
  intervalId.value = null;
};

const clear = () => {
  time.value = 0;
  stop();
};

const countUp = () => {
  intervalId.value = setInterval(() => {
    time.value++;
  }, 1000);
};

const handleCount = () => (isCountingUp.value ? stop() : start());
</script>

<template>
  <div class="flex justify-center items-center flex-col min-h-screen">
    <span class="text-[100px] font-bold">
      {{ time }}
    </span>
    <div class="flex">
      <v-btn
        color="yellow"
        style="margin-right: 10px"
        variant="tonal"
        @click="clear"
        >Clear</v-btn
      >
      <v-btn
        :color="isCountingUp ? 'red' : 'blue'"
        variant="tonal"
        @click="handleCount"
        >{{ isCountingUp ? "Stop" : "Start" }}</v-btn
      >
    </div>
  </div>
</template>
