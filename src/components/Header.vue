<template>
  <div class="container">
    <div class="box">
      <div class="compass">
        <div class="int">
          <div class="section a" />
          <div class="section b" />
          <div class="section c" />
          <div class="section d" />
        </div>
      </div>
      <h1 class="gradient-text">RACIST</h1>
      <div class="desc">Znajdź kolor, który nie pasuje</div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({})
</script>

<style scoped lang="scss">
@import '@/styles/index.scss';
.container {
  background-size: cover;
  border-radius: 10px;
  margin: 2rem auto;
  max-width: 90%;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.box {
  width: 100%;
  max-width: 304px;
  background: #e3e3e377;
  border: 1px solid #e3e3e344;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem 1.5rem;
  position: relative;
}

.gradient-text {
  font-size: clamp(2rem, 8vw, 4rem); // dynamiczna wielkość tekstu
  font-weight: 900;
  text-transform: uppercase;
  background: linear-gradient(-45deg, #ff4e50, #f9d423, #1fb1a3, #2c82ff);
  background-size: 100% auto;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  color: transparent;
  margin: 0;
  padding-top: 20px;
  text-align: center;

  &::before {
    content: 'RACIST';
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    z-index: -1;
    color: rgba(0, 0, 0, 0.4);
    filter: blur(3px);
  }
}

.desc {
  font-size: clamp(0.9rem, 2.5vw, 1.1rem);
  font-weight: 500;
  color: #555;
  margin: 0.5rem 0 0;
  text-align: center;
}

.compass {
  width: 80px;
  height: 80px;
  position: absolute;
  border: 1px solid #ddd;
  background: #e3e3e3;
  padding: 5px;

  top: -40px;
  border-radius: 50%;
}

.int {
  width: 100%;
  height: 100%;
  position: relative;
  border-radius: 50%;
  display: grid;
  overflow: hidden;
  grid-template-areas:
    'a b'
    'c d';
  grid-template-columns: 1fr 1fr;
  gap: 0;

  .section {
    box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2),
      inset 0 0 10px rgba(255, 255, 255, 0.2);
  }

  .a {
    grid-area: a;
    background: #fc5a57;
  }
  .b {
    grid-area: b;
    background: #12b7b7;
  }
  .c {
    grid-area: c;
    background: #fdbf3e;
  }
  .d {
    grid-area: d;
    background: #1a9fbb;
  }
}

@media (max-width: 400px) {
  .box {
    padding: 0.5rem;
  }
  .gradient-text {
    font-size: 2rem;
  }
  .desc {
    font-size: 0.9rem;
  }
}
</style>
