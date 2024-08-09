<template>
  <div class="box">
    <img src="@/assets/high.png" />
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
      max: localStorage.getItem('maxscore'),
    }
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
}
</style>
