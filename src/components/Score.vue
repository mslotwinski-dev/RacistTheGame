<template>
  <div>Wynik: {{ score }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    score: String,
  },
})
</script>

<style lang="scss" scoped>
@import '@/styles/index.scss';

div {
  font-size: 25px;
  font-weight: 600;
  margin: 10px;
}
</style>
