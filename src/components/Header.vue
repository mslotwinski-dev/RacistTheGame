<template>
  <div>
    <span>Racist</span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({})
</script>

<style scoped lang="scss">
@import '@/styles/index.scss';
div {
  display: flex;
  justify-content: center;
  text-transform: uppercase;
  font-size: calc(40px + 2vw);
  font-weight: 800;
  margin: 10px;
  padding: 10px;
  margin-top: 40px;
}
span {
  background: theme(dark);
  padding: 10px 30px;
  color: theme(light);
  border-radius: 20px;
}
</style>
