<template>
  <div class="calc">
    <div class="display">{{ current || '0'}}</div>
    <div @click="clear()" class="btn special-button">AC</div>
    <div @click="sign()" class="btn special-button">+/-</div>
    <div @click="percent()" class="btn special-button">%</div>
    <div @click="divide()" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply()" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="substract()" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add()" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot()" class="btn">.</div>
    <div @click="equal()" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current == ""
        ? this.clear()
        : (this.current =
            this.current.charAt(0) === "-"
              ? this.current.slice(1)
              : `-${this.current}`);
    },
    percent() {
      this.current =
        this.current == "" || this.current == "NaN"
          ? (this.current = "")
          : (this.current = `${parseFloat(this.current) / 100}`);
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    substract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = "";
    }
  }
};

/*
Don't allow multiple 0 at the start
run equal each time operator is clicked
*/
</script>

<style scoped>
.calc {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  justify-items: center;
  font-size: 1.25em;
  height: 350px;
  width: 250px;
  margin: 0 auto;
  overflow: hidden;
  border-radius: 5px;
}

.display {
  width: 100%;
  display: grid;
  align-items: end;
  justify-content: end;
  grid-column: 1 / -1;
  background-color: #4c4c4c;
  font-size: 1.75em;
  color: white;
  padding: 0 20px 5px 0;
  border: 1px solid black;
}

.display > * {
  padding: 15px;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  height: 100%;
  width: 100%;
  display: grid;
  align-items: center;
  background-color: #888484;
  color: white;
  border: 1px #999 solid;
}

.special-button {
  background-color: #615f5f;
}

.operator {
  background-color: #f7a104;
  color: white;
}
</style>



