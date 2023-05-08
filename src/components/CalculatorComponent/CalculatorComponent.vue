<script>
export default {
  name: 'CalculatorComponent',
  data() {
    return {
      number1: '0',
      number2: '',
      operation: '',
      isCalculated: false,
      result: 0,
      order: [7, 8, 9, 4, 5, 6, 1, 2, 3],
    }
  },
  methods: {
    addNumber(num) {
      if (!this.isCalculated && this.number1 === '0') {
        this.number1 = num.toString();
      } else if (!this.isCalculated && this.number1.length < 7) {
        this.number1 += num.toString();
      } else if (this.number2.length < 7) {
        this.number2 += num.toString();
      }
    },
    addComa() {
      if (!this.isCalculated && this.number1.indexOf('.') === -1) {
        this.number1 += '.';
      } else if (this.number2.indexOf('.') === -1) {
        this.number2 += '.';
      }
    },
    toggleSign() {
      if (!this.isCalculated) {
        this.number1 = +this.number1 * -1;
      } else {
        this.number2 = +this.number2 * -1;
      }
    },
    findPercent() {
      if (!this.isCalculated) {
        this.number1 = +this.number1 / 100;
      } else {
        this.number2 = +this.number2 / 100;
      }
    },
    clear() {
      this.number1 = '0';
      this.number2 = '';
      this.operation = '';
      this.isCalculated = false;
    },
    setOperation(str) {
      if (this.operation === str) {
        this.operation = '';
        this.isCalculated = false;
        this.number2 = '';
      } else {
        this.operation = str;
        this.isCalculated = true;
        this.number2 = '';
      }
    },
    calculate() {
      switch (this.operation) {
        case '+':
          this.result = +this.number1 + +this.number2;
          break;
        case '-':
          this.result = +this.number1 - +this.number2;
          break;
        case '*':
          this.result = +this.number1 * +this.number2;
          break;
        case '/':
          this.result = +this.number1 / +this.number2;
          break;
        default:
          return;
      }
      if (Math.abs(this.result) >= 1e7) {
        this.number1 = this.result.toExponential(4);
      } else { 
        this.number1 = this.result
      }
      this.result = 0;
      this.isCalculated = false;
    },
  },
}
</script>

<template>
  <div class="screen">
    <div class="screen__result">
      <p :class="{ 'screen__result-small': number2 > 10000000 }" v-if="isCalculated && number2">{{ number2 }}</p>
      <p :class="{ 'screen__result-small': number1 > 10000000 }" v-else>{{ number1 }}</p>
    </div>
    <div class="screen__buttons">
      <div class="screen__buttons-numbers">
        <button class="button button__add" @click="clear()">
          <p v-if="number1 !== '0'">C</p>
          <p v-else>AC</p>
        </button>
        <button class="button button__add" @click="toggleSign()">
          +/-
        </button>
        <button class="button button__add" @click="findPercent()">
          %
        </button>
        <div v-for="(item, index) in order" :key="index">
          <button class="button" @click="addNumber(item)">
            {{ item }}
          </button>
        </div>
        <button class="button button__custom" @click="addNumber(0)">
            0
        </button>
        <button class="button" @click="addComa()">
          .
        </button>
      </div>
      <div class="screen__buttons-actions">
        <button :class="{ 'active': operation === '/' }" class="button button__action" @click="setOperation('/')">
          ÷
        </button>
        <button :class="{ 'active': operation === '*' }" class="button button__action" @click="setOperation('*')">
          ×
        </button>
        <button :class="{ 'active': operation === '-' }" class="button button__action" @click="setOperation('-')">
          -
        </button>
        <button :class="{ 'active': operation === '+' }" class="button button__action" @click="setOperation('+')">
          +
        </button>
        <button class="button button__action" @click="calculate()">
          =
        </button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './CalculatorComponent.scss';
</style>