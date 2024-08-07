<template>
  <div class="cont">
    <img src="@/assets/timer.png" alt="" />
    <div class="bar">
      <div class="time" :style="{ width: `${(100 * time) / max}%` }" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    time: Number,
    max: Number,
  },
})
</script>

<style lang="scss" scoped>
@import '@/styles/index.scss';
.cont {
  display: flex;
  align-items: center;
  max-height: 80px;
}
.bar {
  width: 400px;
  flex-shrink: 1;
  height: 40px;

  border-radius: 10px;
  @media (max-width: 1000px) {
    width: 250px;
  }
}
.time {
  width: 100%;
  height: 100%;
  background: theme(main);
  border-radius: 8px;
  transition: 0.2s all;
}

img {
  width: 30px;
  height: 30px;
  margin-right: 10px;
}
</style>
