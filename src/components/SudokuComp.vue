<template>
    <button @click="start(arg, event)" class="btn">sudoku</button>

  <div class="container">
    <div class="board">
      <div class="item" v-for="index in arr" :key="index"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      levels: [],
      arr: [],
    };
  },
  methods: {
    start(){
        this.arr = [];
        this.fillArr();
    },
    fillArr(){
        for (let i = 0; i < 81; i++) {
            this.arr.push(i);            
        }
    }
  },
  created() {},
};
</script>

<style lang="css" scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh; /* 100% высоты экрана */
}

.board {
    display: grid;
    grid-template-columns: repeat(9, 1fr);
    grid-template-rows: repeat(9, 1fr);
    width: 450px; /* 9 * 50px (ширина и высота каждого элемента) */
    height: 450px;
    gap: 1px;
    margin-top: 16px;
    position: relative;
}

.item {
    width: 100%;
    height: 100%;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
}

.board::before,
.board::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    border: 2px solid black;
    pointer-events: none; 
}

.board::before {
    border-width: 0 2px;
    top: calc(1 / 3 * 100%);
    bottom: calc(1 / 3 * 100%);
}

.board::after {
    border-width: 2px 0;
    left: calc(1 / 3 * 100%);
    right: calc(1 / 3 * 100%);
}
</style>
