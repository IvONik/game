<template>
  <div>
    
    <h3 class="ruls">Правила
      <span class="ruls__text">У вас есть два ряда бобов серый и цветной, серые скрывают правильную последованность ваша задача переставить цветные бобы в правильном порядке который скрывает серые бобы.
        </span>
    </h3>
    
    <div class="buttons">
      <button @click="start" class="btn">Старт</button>

      <select class="btn" v-model="selectedOption" @change="selectLevel">
        <option value="choose" disabled hidden>Выбрать уровень</option>
        <option value="1">Level 1</option>
        <option value="2">Level 2</option>
        <option value="3">Level 3</option>
      </select>

      <button @click="showHint" class="btn">подсказкa</button>
    </div>

    <div class="score">количество совпадений: {{ count }}</div>

    <div class="board">
      <div
        v-for="(item, index) in arr1"
        :key="index"
        :class="['bob', getClass(item), { active: index === activeIndex }]"
        class="bob"
        @click="selectItem(index)"
      ></div>
    </div>

    <div class="board answer" 
    >
      <div
        v-for="(item, index) in arr2"
        :key="index"
        :class="[getClass(item), { hint: index === showIndex }]"
        class="bob light "
      >
        {{}}
      </div>
    </div>
    <div class="finish" v-if="isfinnish">WIN !!!</div>
    <div class="score" v-if="isfinnish">
      количество ходов: {{ numbersOfMoves }}
    </div>
    <div class="score" v-if="isfinnish">
      использовано подсказок: {{ numbersOfClue }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr1: [],
      arr2: [],
      currentLevel: 1,
      level: [6, 9, 12],
      selectedItemIndex1: null,
      selectedItemIndex2: null,
      count: 0,
      isfinnish: false,
      numbersOfMoves: 0,
      activeIndex: null,
      selectedOption: "choose",
      showIndex: null,
      numbersOfClue: 0,
    };
  },
  methods: {
    start() {
      this.numbersOfClue = 0;
      this.isfinnish = false;
      this.count = 0;
      this.numbersOfMoves = 0;
      this.activeIndex = null;
      this.arr1 = new Array(this.level[this.currentLevel - 1])
        .fill(0)
        .map((_, index) => index + 1);
      this.shuffleArray(this.arr1);
      this.arr2 = new Array(this.level[this.currentLevel - 1])
        .fill(0)
        .map((_, index) => index + 1);
      this.shuffleArray(this.arr2);
      this.countMatches();
    },
    shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
    },
    selectItem(index) {
      if (this.selectedItemIndex1 === null) {
        this.selectedItemIndex1 = index;
        this.activeIndex = index;
      } else {
        this.selectedItemIndex2 = index;
        const temp = this.arr1[this.selectedItemIndex1];
        this.arr1[this.selectedItemIndex1] = this.arr1[this.selectedItemIndex2];
        this.arr1[this.selectedItemIndex2] = temp;
        this.selectedItemIndex1 = null;
        this.selectedItemIndex2 = null;
        this.countMatches();
        this.numbersOfMoves++;
        if (this.count === this.arr1.length) {
          this.isfinnish = true;
        }
        this.activeIndex = null;
      }
    },
    countMatches() {
      this.count = 0;
      for (let i = 0; i < this.arr1.length; i++) {
        if (this.arr1[i] === this.arr2[i]) {
          this.count++;
        }
      }
    },
    getClass(item) {
      if (item === 1) {
        return "color1";
      } else if (item === 2) {
        return "color2";
      } else if (item === 3) {
        return "color3";
      } else if (item === 4) {
        return "color4";
      } else if (item === 5) {
        return "color5";
      } else if (item === 6) {
        return "color6";
      } else if (item === 7) {
        return "color7";
      } else if (item === 8) {
        return "color8";
      } else if (item === 9) {
        return "color9";
      } else if (item === 10) {
        return "color10";
      } else if (item === 11) {
        return "color11";
      } else if (item === 12) {
        return "color12";
      }
    },
    selectLevel() {
      if (this.selectedOption === "1") {
        this.currentLevel = 1;
      } else if (this.selectedOption === "2") {
        this.currentLevel = 2;
      } else {
        this.currentLevel = 3;
      }
      this.start();
    },
    showAnswer() {
      this.isfinnish = true;
    },
    showHint() {
      this.numbersOfClue++;
      this.showIndex = Math.floor(Math.random() * this.arr2.length);
      setTimeout(() => {
        this.showIndex = null;
      }, 1000);
    },
  },
  mounted() {
    this.start();
  },
};
</script>

<style lang="css" scoped>
.ruls {
  position: relative;
  margin-left: auto;
  margin-right: auto;
  width: 300px;
  cursor: pointer;
}

.ruls__text {
  visibility: hidden;
  width: 300px;
  background-color: #555;
  color: #fff; 
  text-align: center;
  border-radius: 10px;
  padding: 10px;
  position: absolute;
  top: 120%;
  left: 50%;
  margin-left: -150px;
  opacity: 0;
  transition: opacity 0.3s;
  z-index: 1;
}

.ruls__text::after {
  content: '';
  position: absolute;
  top: -100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

.ruls:hover .ruls__text {
  visibility: visible;
  opacity: 1;
}

.btn {
  font-size: 22px;
  background-color: #fff;
  border-radius: 10px;
  border: 1px solid gray;
  margin: 4px;
  margin-bottom: 16px;
}
.btn:hover{
  background-color: rgb(207, 231, 239);
  transition: 0.4s;
}
.score {
  font-size: 18px;
  margin-bottom: 16px;
}
.bob {
  display: flex;
  width: 30px;
  height: 60px;
  gap: 10px;
  border: none;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  border-radius: 15px;
  box-sizing: border-box;
  position: relative;
}
.bob.light::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 10px;

  background-color: rgb(155, 154, 154);
  opacity: 1;
  z-index: 1;
  transition: opacity 0.5s ease;
}
.bob.light.hint::before {
  opacity: 0;
}
.board {
  display: flex;
  justify-content: center;
  gap: 5px;
  margin-bottom: 12px;
}
.active {
  border: 3px dashed black;
}
.color1 {
  background-color: red;
}
.color2 {
  background-color: rgb(100, 149, 44);
}
.color3 {
  background-color: rgb(237, 170, 14);
}
.color4 {
  background-color: rgb(195, 42, 164);
}
.color5 {
  background-color: rgb(228, 53, 214);
}
.color6 {
  background-color: rgb(113, 91, 164);
}
.color7 {
  background-color: rgb(8, 242, 211);
}
.color8 {
  background-color: rgb(165, 174, 133);
}
.color9 {
  background-color: rgb(207, 245, 93);
}
.color10 {
  background-color: rgb(138, 49, 65);
}
.color11 {
  background-color: rgb(215, 160, 173);
}
.color12 {
  background-color: rgb(237, 230, 4);
}
.light {
  z-index: 0;
}
</style>
