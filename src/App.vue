<template>
  <div class="container">
    <h1>Número Aleatorio y Hanzi</h1>
    <div class="difficulty-switch">
      <label for="easy">Fácil</label>
      <input
        type="radio"
        id="easy"
        value="easy"
        v-model="difficulty"
        @change="updateDisplay"
      />
      <label for="medium">Intermedio</label>
      <input
        type="radio"
        id="medium"
        value="medium"
        v-model="difficulty"
        @change="updateDisplay"
      />
      <label for="hard">Difícil</label>
      <input
        type="radio"
        id="hard"
        value="hard"
        v-model="difficulty"
        @change="updateDisplay"
      />
    </div>
    <div class="number-container">
      <div class="topSection">
        {{ top }}
      </div>
      <h2 class="downSection">{{ down }}</h2>
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #333;
  color: #fff;
  text-align: center;
}

.difficulty-switch {
  margin-bottom: 2rem;
}

.difficulty-switch label {
  margin-right: 1rem;
}

.number-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 50%;
  max-width: 600px;
}

.topSection {
  font-size: 10vw;
  font-weight: bold;
  margin-bottom: 2rem;
}

.downSection {
  font-size: 6vw;
}
</style>

<script>
export default {
  name: "App",
  data() {
    return {
      top: "",
      down: "",
      difficulty: "easy",
    };
  },
  methods: {
    getRandomNumber(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    getHanzi(number) {
      const hanziList = [
        "一",
        "二",
        "三",
        "四",
        "五",
        "六",
        "七",
        "八",
        "九",
        "十",
        "十一",
        "十二",
        "十三",
        "十四",
        "十五",
        "十六",
        "十七",
        "十八",
        "十九",
        "二十",
        "二十一",
        "二十二",
        "二十三",
        "二十四",
        "二十五",
        "二十六",
        "二十七",
        "二十八",
        "二十九",
        "三十",
        "三十一",
        "三十二",
        "三十三",
        "三十四",
        "三十五",
        "三十六",
        "三十七",
        "三十八",
        "三十九",
        "四十",
        "四十一",
        "四十二",
        "四十三",
        "四十四",
        "四十五",
        "四十六",
        "四十七",
        "四十八",
        "四十九",
        "五十",
        "五十一",
        "五十二",
        "五十三",
        "五十四",
        "五十五",
        "五十六",
        "五十七",
        "五十八",
        "五十九",
        "六十",
        "六十一",
        "六十二",
        "六十三",
        "六十四",
        "六十五",
        "六十六",
        "六十七",
        "六十八",
        "六十九",
        "七十",
        "七十一",
        "七十二",
        "七十三",
        "七十四",
        "七十五",
        "七十六",
        "七十七",
        "七十八",
        "七十九",
        "八十",
        "八十一",
        "八十二",
        "八十三",
        "八十四",
        "八十五",
        "八十六",
        "八十七",
        "八十八",
        "八十九",
        "九十",
        "九十一",
        "九十二",
        "九十三",
        "九十四",
        "九十五",
        "九十六",
        "九十七",
        "九十八",
        "九十九",
      ];

      if (number >= 1 && number <= 99) {
        return hanziList[number - 1];
      } else {
        return "Número inválido";
      }
    },
    updateDisplay() {
      const randomNumber = this.getRandomNumber(1, 99);
      const hanzi = this.getHanzi(randomNumber);
      this.top = this.difficulty === "easy" ? randomNumber : hanzi;
      this.down =
        this.difficulty === "easy"
          ? hanzi
          : this.difficulty === "medium"
          ? randomNumber
          : "";
    },
    handleKeyPress(event) {
      if (event.keyCode === 32) {
        // Código de la tecla Spacebar
        this.updateDisplay();
      }
    },
  },
  mounted() {
    document.addEventListener("keydown", this.handleKeyPress);
  },
  beforeUnmount() {
    document.removeEventListener("keydown", this.handleKeyPress);
  },
};
</script>

