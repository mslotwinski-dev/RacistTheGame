<template>
  <div class="box">
    <img src="@/assets/high.png" alt="high score" />
    <div>
      Najwyższy wynik:
      {{ max }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      max: Number(localStorage.getItem('maxscore')) || 0,
    }
  },
  mounted() {
    window.addEventListener('storage', this.updateMax)
  },
  beforeUnmount() {
    window.removeEventListener('storage', this.updateMax)
  },
  methods: {
    updateMax() {
      this.max = Number(localStorage.getItem('maxscore')) || 0
    },
  },
})
</script>

<style lang="scss" scoped>
@import '@/styles/index.scss';

.box {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

img {
  height: 30px;
  margin-right: 8px;
}
</style>
