<template>
  <div class="calculator">
    <div class="screen">
      <div class="input_result">{{ display }}</div>
    </div>
    <div class="content">
      <div
        class="key misc"
        @click="clear"
      >
        AC
      </div>
      <div
        class="key misc b-left"
        @click="changeSign"><sup>+</sup>/<sub>-</sub></div>
      <div
        class="key misc b-left"
        @click="calculatePercentage">%</div>
      <div
        class="key op operator b-left"
        @click="clickOperator">/</div>
      <div
        class="key num b-top"
        @click="clickNum">7</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">8</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">9</div>
      <div
        class="key op operator b-left b-top"
        @click="clickOperator">*</div>
      <div
        class="key num b-top"
        @click="clickNum">4</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">5</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">6</div>
      <div
        class="key op operator b-left b-top"
        @click="clickOperator">-</div>
      <div
        class="key num b-top"
        @click="clickNum">1</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">2</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">3</div>
      <div
        class="key op operator b-left b-top"
        @click="clickOperator">+</div>
      <div
        class="key num wide b-top b-bottom-left-radius"
        @click="clickNum">0</div>
      <div
        class="key num b-left b-top"
        @click="clickNum">.</div>
      <div
        class="key op b-left b-top b-bottom-right-radius equal"
        @click="clickEqual">=</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      button: '',
      display: 0,
      num1: null,
      num2: null,
      operator: null,
      operatorSelected: false,
      total: null
    }
  },
  methods: {
    calculateTotal() {
      if (this.num2) {
        return eval(this.num1 + this.operator + this.num2)
      }
      return this.num1
    },
    calculatePercentage() {
      this.total /= 100
      if (this.operatorSelected) {
        this.num2 = this.total
      } else {
        this.num1 = this.total
      }
      this.display = this.total
    },
    clear() {
      this.button = ''
      this.display = 0
      this.num1 = null
      this.num2 = null
      this.operator = null
      this.operatorSelected = false
      this.total = null
    },
    clickEqual() {
      if (this.num1 && this.num2) {
        this.total = this.calculateTotal()
        this.display = this.total
        this.button = this.total
      }
    },
    clickNum(event) {
      this.button += event.target.textContent
      this.display = this.button
      if (this.operatorSelected) {
        this.num2 = this.button
      } else {
        this.num1 = this.button
      }
      this.total = this.button
    },
    clickOperator(event) {
      if (this.operatorSelected) {
        this.total = this.calculateTotal()
        this.display = this.total
        this.num1 = this.total
      }
      this.operatorSelected = true

      this.operator = event.target.textContent
      this.button = ''
    },
    changeSign() {
      this.total *= -1
      if (this.operatorSelected) {
        this.num2 = this.total
      } else {
        this.num1 = this.total
      }
      this.display = this.total
    }
  }
}
</script>

<style lang="scss">
$light-grey: #e4e4e4;
$grey: #d5d5d5;
$border-grey: #afafaf;
$orange: #f68f24;
$light-orange: #ffae59;

/* MAIN */

* {
  margin: 0;
  padding: 0;
}

html,
body {
  min-height: 100%;
}

body {
  background: linear-gradient(180deg, #5494af, #eaa75a);
  font-family: 'HelveticaNeue-UltraLight', 'Helvetica Ultra Light',
    'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 20px;
}

.calculator {
  width: 231px;
  height: 310px;
  box-shadow: 0 10px 30px #4e4e4e;
  position: absolute;
  left: 50%;
  top: 50%;
  margin: -155px 0 0 -115.5px;
}

/* SCREEN */

.screen {
  width: 100%;
  height: 85px;
  background-color: rgba(#333333, 0.8);
  text-align: right;
  position: relative;
  overflow: hidden;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
}

.input_result {
  background-color: transparent;
  width: 90%;
  font-size: 45px;
  color: #fff;
  text-align: right;
  border: none;
  padding-top: 30px;
}

/* BUTTONS */

.key {
  float: left;
  vertical-align: center;
  text-align: center;
  padding: 0;
  margin: 0;
  width: 57px;
  height: 45px;
  line-height: 45px;
  background-color: $light-grey;
  cursor: pointer;

  &:hover {
    background-color: #f2f2f2;
  }

  &:active {
    background: rgba(255, 255, 255, 0.8);
  }
}

.misc {
  background-color: $grey;
}

.op {
  background-color: $orange;
  color: #fff;

  &:hover {
    background-color: $light-orange;
  }

  &:active {
    background: rgba(255, 255, 255, 0.2);
  }
}

.wide {
  width: 115px;
}

/* BORDERS */

.b-left {
  border-left: 1px solid $border-grey;
}

.b-top {
  border-top: 1px solid $border-grey;
}

/* BORDER RADIUS */

.b-bottom-left-radius {
  border-bottom-left-radius: 5px;
}

.b-bottom-right-radius {
  border-bottom-right-radius: 5px;
}
</style>
