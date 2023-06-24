<template>
  <div @click="handleClick" @keydown.space="handleSpacebar" @touchstart="handleTouchStart">
    <v-app>
      <v-main>
        <v-container class="container">
          <v-row align="center">
            <v-col cols="12" md="12" lg="12" sm="12">
              <v-select
                    v-model="difficulty"
                    :items="difficultyOptions"
                    label="Dificultad"
                    @change="updateDisplay"
                    filled
                    dark
                  ></v-select>
            </v-col>
          </v-row>
          <div>
            <v-row align="center">
              <v-col cols="12" md="12" lg="12" sm="12">
                <div class="top-section" :class="topSectionClass">
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
  </div>
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
  .top-section-content-easy {
    font-size: 50vw;
  }

  .top-section-content-medium {
    font-size: 30vw;
  }

  .top-section-content-hard {
    font-size: 30vw;
  }
}

@media (min-width: 768px) {
  /* Estilos para pantallas de escritorio */
  .top-section-content-easy {
    font-size: 20vw;
  }

  .top-section-content-medium {
    font-size: 20vw;
  }

  .top-section-content-hard {
    font-size: 25vw;
  }
}


.down-section {
  font-size: 8vw;
  text-align: center;
  width: 100%;
}
</style>

<script>
import * as cn from "chinese-numbering";

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
      topSectionClass: "top-section-content-easy"
    };
  },
  methods: {
    getRandomNumber(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    getHanzi(number) {
      if (number >= 1 && number <= 99) {
        return cn.numberToChinese(number);
      } else {
        return "Número inválido";
      }
    },
    updateDisplay() {
      const randomNumber = this.getRandomNumber(1, 99);
      const hanzi = this.getHanzi(randomNumber);

      if (this.difficulty === "easy") {
        this.topSection = randomNumber;
        this.topSectionClass = "top-section-content-easy";
      } else if (this.difficulty === "medium") {
        this.topSection = hanzi;
        this.topSectionClass = "top-section-content-medium";
      } else if (this.difficulty === "hard") {
        this.topSection = hanzi;
        this.topSectionClass = "top-section-content-hard";
      }
      this.downSection =
        this.difficulty === "easy"
          ? hanzi
          : this.difficulty === "medium"
          ? randomNumber
          : "";
    },
    handleSpacebar() {
      this.updateDisplay();
    },
    handleTouchStart() {
      this.touchStartTime = new Date().getTime();
    },
    handleTouchEnd() {
      const touchEndTime = new Date().getTime();
      const touchDuration = touchEndTime - this.touchStartTime;
      if (touchDuration < 500) {
        this.updateDisplay();
      }
    },
    handleClick() {
      this.topSection = 'Qua k'
      if (!this.isLaptop()) {
        this.updateDisplay();
      }
    },
    isLaptop() {
      const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
      return !isMobile;
    },
  },
  mounted() {
    document.addEventListener("keydown", this.handleSpacebar);
  },
  beforeUnmount() {
    document.removeEventListener("keydown", this.handleSpacebar);
  },
};
</script>
