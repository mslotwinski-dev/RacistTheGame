<template>
  <div class="home">
    <Header />
    <Grid />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Header from '@/components/Header.vue'
import Grid from '@/components/Grid.vue'

export default defineComponent({
  name: 'HomeView',
  components: {
    Header,
    Grid,
  },
})
</script>

<style lang="scss" scoped>
.home {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
