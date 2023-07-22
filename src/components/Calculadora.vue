<template>
  <div class="calculadora">
    <Display :value="displayValue" />
    <Botao label="AC" triple @onClick="clearMemory" />
    <Botao label="/" operation @onClick="setOperation" />
    <Botao label="7" @onClick="addDigit" />
    <Botao label="8" @onClick="addDigit" />
    <Botao label="9" @onClick="addDigit" />
    <Botao label="*" operation @onClick="setOperation" />
    <Botao label="4" @onClick="addDigit" />
    <Botao label="5" @onClick="addDigit" />
    <Botao label="6" @onClick="addDigit" />
    <Botao label="-" operation @onClick="setOperation" />
    <Botao label="1" @onClick="addDigit" />
    <Botao label="2" @onClick="addDigit" />
    <Botao label="3" @onClick="addDigit" />
    <Botao label="+" operation @onClick="setOperation" />
    <Botao label="0" double @onClick="addDigit" />
    <Botao label="." @onClick="addDigit" />
    <Botao label="=" operation @onClick="setOperation" />
  </div>
</template>

<script>
import Botao from "./Botao.vue";
import Display from "./Display.vue";

export default {
  name: "Calculadora",
  data: function () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operatio: null,
      values: [0, 0],
      current: 0,
    };
  },
  components: { Botao, Display },
  methods: {
    clearMemory() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;
        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
          if (isNaN(this.values[0]) || !isFinite(this.values[0])) {
            this.clearMemory();
            return;
          }
        } catch (e) {
          this.$emit("onError", e);
        }

        this.values[1] = 0;
        this.displayValue = this.values[0];
        this.operatio = equals ? null : operation;
        this.current = equals ? 0 : 1;
        this.clearDisplay = !equals;
      }
    },
    addDigit(n) {
      if (n == "." && this.displayValue.includes(".")) {
        return;
      }
      const clearDisplay = this.displayValue === "0" || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + n;
      this.displayValue = displayValue;
      this.clearDisplay = false;

      if (n !== ".") {
        const i = this.current;
        const newValue = parseFloat(displayValue);
        this.values[i] = newValue;
      }
    },
  },
};
</script>

<style>
.calculadora {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;
  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>