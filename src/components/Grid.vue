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
            :style="{ backgroundColor: `#${r}${g}${b}` }"
          >
            <div
              class="wrong"
              v-if="i == wrongy && j == wrongx"
              :style="{ background, opacity }"
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
      r: '0',
      g: '0',
      b: '0',
      background: 'black',
      opacity: 0.5,
      restart: 0,
      time: 50,
      MAX_TIME: 50,
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

      this.opacity = 0.35 * Math.pow(1.075, -this.score) + 0.01
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

      const r = this.rand(30, 225)
      const g = this.rand(30, 225)
      const b = this.rand(30, 225)
      this.r = r.toString(16)
      this.g = g.toString(16)
      this.b = b.toString(16)

      this.wrongx = this.rand(1, this.size)
      this.wrongy = this.rand(1, this.size)

      r <= 50 || g <= 50 || b <= 50
        ? (this.background = 'white')
        : (this.background = 'black')
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
      this.generate()
    },
    timer() {
      if (this.score != 0) this.time--
      else this.time = this.MAX_TIME
      if (this.time == 0) this.lose()
    },
  },
  mounted() {
    this.generate()

    window.setInterval(() => {
      this.timer()
    }, 100)
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
