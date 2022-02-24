<template>
  <div class="wrapper">
    <div class="calc-body">
      <div v-if="operator == ''" class="action">{{ value || 0 }}</div>
      <div v-else class="action">{{ previousValue || 0 }} {{ operator }} {{ value || 0 }}</div>

      <div
        v-for="item in buttons"
        :key="item"
        class="calc_button"
        :class="{ task: ['*', '/', '-', '+'].includes(item) }"
        @click="actionTask(item)"
      >
        {{ item }}
      </div>

      <div class="calc_button task_end" @click="actionTask(taskEnd)">=</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "vCalc",
  props: {},
  data() {
    return {
      value: "",
      previousValue: "",
      operator: "",
      buttons: ["+", "-", "/", "*", "1", "2", "3", "4", "5", "6", "7", "8", "9", "0"],
      taskEnd: "taskEnd"
    };
  },
  methods: {
    actionTask(item) {
      console.log(item);

      if (!isNaN(item) || item === ".") {
        this.value += item + "";
      }
      if (["/", "*", "-", "+"].includes(item)) {
        this.operator = item;
        this.previousValue = this.value;
        this.value = "";
      }
      if (item === this.taskEnd) {
        this.value = eval(this.previousValue + this.operator + this.value);
        this.previousValue = "";
        this.operator = "";
      }
    }
  },
  mounted() {
    document.addEventListener("keydown", (event) => {
      if (event.code === "Enter") {
        this.actionTask(this.taskEnd);
      }
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
}
.calc-body {
  background: rgb(90, 90, 90);
  width: 800px;
  height: 900px;
  border: 1px solid black;
  display: grid;
  grid-template-columns: repeat(auto-fill, 200px);
}
.calc_button {
  color: white;
  padding: 15px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgb(60, 60, 60);
  border: 1px solid rgb(160, 160, 160);
  font-size: 25px;
}
.calc-body .calc_button:nth-last-child(1) {
  border: 1px solid rgba(143, 248, 255, 0.528);
}
.calc_button:hover {
  background: rgb(90, 90, 90);
  cursor: pointer;
}
.task {
  background: rgb(77, 77, 77);
}
.action {
  grid-column: span 4;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30px;
}
.migaet {
}
</style>
