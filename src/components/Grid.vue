<template>
  <div class="container">
    <Bar v-if="score != 0" :key="restart" :time="time" :max="MAX_TIME" />
    <MaxScore :key="restart" />
    <Score :score="score" />

    <div class="grid" :key="restart">
      <div class="column" v-for="i in size" :key="i">
        <div class="row" v-for="j in size" :key="j">
          <div
            class="ball"
            :class="`size${size}`"
            :style="{ backgroundColor: baseColor }"
          >
            <div
              class="wrong"
              v-if="i == wrongy && j == wrongx"
              :style="{ backgroundColor: wrongColor }"
              @click="won()"
            />
            <div class="clean" @click="lose()" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import Score from './Score.vue'
import Bar from './Bar.vue'
import MaxScore from './MaxScore.vue'

export default defineComponent({
  components: { Score, Bar, MaxScore },
  data() {
    return {
      score: 0,
      size: 2,
      wrongx: 0,
      wrongy: 0,
      baseColor: '',
      wrongColor: '',
      background: 'black',
      opacity: 0.5,
      restart: 0,
      time: 50,
      MAX_TIME: 50,
      interval: null as number | null,
    }
  },
  methods: {
    rand(min: number, max: number) {
      return Math.floor(Math.random() * (max - min + 1) + min)
    },

    stats() {
      if (this.score == 0) this.size = 2
      if (this.score == 5) this.size = 3
      if (this.score == 10) this.size = 4
      if (this.score == 15) this.size = 5
      if (this.score == 20) this.size = 6

      // ograniczenie opacity do przedziału [0.05, 0.5]
      this.opacity = Math.min(
        0.5,
        Math.max(0.05, 0.35 * Math.pow(1.075, -this.score) + 0.01)
      )
    },

    maxscore() {
      if (!localStorage.maxscore) localStorage.maxscore = 0
      localStorage.maxscore = Math.max(
        this.score,
        Number(localStorage.maxscore)
      )
    },

    generate() {
      this.stats()
      this.restart++
      this.maxscore()

      // Losowy ładny pastelowy kolor w HSL
      const h = this.rand(0, 360) // hue
      const s = this.rand(60, 80) // saturation
      const l = this.rand(40, 60) // lightness (ładne pastelowe)

      this.baseColor = `hsl(${h}, ${s}%, ${l}%)`

      // różnica zależna od wyniku (im wyżej, tym trudniej)
      const delta = Math.max(2, 15 - this.score * 0.5) // np. od 15% do 2%

      this.wrongColor = `hsl(${h}, ${s}%, ${l + delta}%)`

      this.wrongx = this.rand(1, this.size)
      this.wrongy = this.rand(1, this.size)
    },

    won() {
      this.score++
      this.generate()

      if (this.score > 40) this.time = this.MAX_TIME + 2
      else if (this.score > 20) this.time = this.MAX_TIME + 1
      else this.time = this.MAX_TIME
    },

    lose() {
      alert('PRZEGRAŁEŚ')
      this.score = 0
      setTimeout(() => this.generate(), 200) // mała pauza
    },

    timer() {
      if (this.score != 0) this.time--
      else this.time = this.MAX_TIME
      if (this.time == 0) this.lose()
    },
  },

  mounted() {
    this.generate()
    this.interval = window.setInterval(() => this.timer(), 100)
  },

  beforeUnmount() {
    if (this.interval) clearInterval(this.interval)
  },
})
</script>

<style lang="scss" scoped>
@import '@/styles/index.scss';
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  flex-grow: 1;
}
.column {
  display: flex;
}
.ball {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin: 10px;
  overflow: hidden;
  cursor: pointer;

  &.size2 {
    margin: 10px;
  }
  &.size3 {
    margin: 8px;
  }
  &.size4 {
    margin: 7px;
  }
  &.size5 {
    margin: 6px;
  }

  &.size6 {
    margin: 5px;
  }

  @media (max-width: 1000px) {
    &.size2 {
      width: 100px;
      height: 100px;
      margin: 10px;
    }
    &.size3 {
      width: 90px;
      height: 90px;
      margin: 8px;
    }
    &.size4 {
      width: 70px;
      height: 70px;
      margin: 6px;
    }
    &.size5 {
      width: 60px;
      height: 60px;
      margin: 5px;
    }

    &.size6 {
      width: 50px;
      height: 50px;
      margin: 3.5px;
    }
  }
}

.wrong {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
}

.clean {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-image: url('@/assets/ball.jpg');
  background-size: cover;
  background-position: center;
  opacity: 0.03;
}
</style>
