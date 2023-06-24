<template>
  <v-app>
    <v-main>
      <v-container class="container">
        <v-row align="center">
          <v-col cols="12" md="12" lg="12">
            <v-form class="form">
              <v-select
                v-model="difficulty"
                :items="difficultyOptions"
                label="Dificultad"
                outlined
                @change="updateDisplay"
              ></v-select>
            </v-form>
          </v-col>
        </v-row>
        <div @touchstart="handleTouchStart" @touchend="handleTouchEnd">
          <v-row align="center">
            <v-col cols="12" md="12" lg="12" sm="12">
              <div class="top-section">
                <div class="top-section-content">
                  {{ topSection }}
                </div>
              </div>
            </v-col>
          </v-row>
          <v-row align="center">
            <v-col cols="12" md="12" lg="12" sm="12">
              <div class="down-section">
                {{ downSection }}
              </div>
            </v-col>
          </v-row>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<style>
.container {
  height: 100vh;
  background-color: #333;
  color: #fff;
  text-align: center;
}

.form {
  margin-bottom: 2rem;
}

.top-section-content {
  font-weight: bold;
  text-align: center;
  width: 100%;
}

@media (max-width: 767px) {
  /* Estilos para dispositivos móviles */
  .top-section-content {
    font-size: 50vw;
  }
}

@media (min-width: 768px) {
  /* Estilos para pantallas de escritorio */
  .top-section-content {
    font-size: 20vw;
  }
}

.down-section {
  font-size: 8vw;
  text-align: center;
  width: 100%;
}
</style>

<script>
export default {
  name: "App",
  data() {
    return {
      topSection: "",
      downSection: "",
      difficulty: "easy",
      touchStartTime: 0,
      difficultyOptions: [
        { text: "Fácil", value: "easy" },
        { text: "Intermedio", value: "medium" },
        { text: "Difícil", value: "hard" },
      ],
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
      this.topSection = this.difficulty === "easy" ? randomNumber : hanzi;
      this.downSection =
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
    handleTouchStart(event) {
      this.touchStartTime = new Date().getTime();
    },
    handleTouchEnd(event) {
      const touchEndTime = new Date().getTime();
      const touchDuration = touchEndTime - this.touchStartTime;
      if (touchDuration < 500) {
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
