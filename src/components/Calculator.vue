<template>
<v-container>
  <v-row align="center" justify="center">
    <v-col>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <v-btn block  tile text @click="clear" class="btn">C</v-btn>
    <v-btn tile text @click="sign" class="btn">+/-</v-btn>
    <v-btn tile text @click="perscent" class="btn">%</v-btn>
    <v-btn tile text @click="divide" class="btn operator">÷</v-btn>
    <v-btn tile text @click="append('7')" class="btn">7</v-btn>
    <v-btn tile text @click="append('8')" class="btn">8</v-btn>
    <v-btn tile text @click="append('9')" class="btn">9</v-btn>
    <v-btn tile text @click="times" class="btn operator">x</v-btn>
    <v-btn tile text @click="append('4')" class="btn">4</v-btn>
    <v-btn tile text @click="append('5')" class="btn">5</v-btn>
    <v-btn tile text @click="append('6')" class="btn">6</v-btn>
    <v-btn tile text @click="minus" class="btn operator">-</v-btn>
    <v-btn tile text @click="append('1')" class="btn">1</v-btn>
    <v-btn tile text @click="append('2')" class="btn">2</v-btn>
    <v-btn tile text @click="append('3')" class="btn">3</v-btn>
    <v-btn tile text @click="add" class="btn operator">+</v-btn>
    <v-btn tile text @click="append('0')" class="btn zero">0</v-btn>
    <v-btn tile text @click="dot" class="btn">.</v-btn>
    <v-btn tile text @click="equal" class="btn operator">=</v-btn>
  </div>
  </v-col>
  </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear () {
      this.current = ''
    },
    sign () {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    perscent () {
      this.current = `${parseFloat(this.current / 100)}`
    },
    append (number) {
      if (this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot () {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevios () {
      this.previous = this.current
      this.operatorClicked = true
    },
    divide () {
      this.operator = (a, b) => a / b
      this.setPrevios()
    },
    times () {
      this.operator = (a, b) => a * b
      this.setPrevios()
    },
    minus () {
      this.operator = (a, b) => a - b
      this.setPrevios()
    },
    add () {
      this.operator = (a, b) => a + b
      this.setPrevios()
    },
    equal () {
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`
      this.previous = null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  text-align: center;
}

.display{
  display: grid;
  grid-column: 1/5;
  background-color: #333;
  color: white;
  text-align: right;
  padding: 10px
}

.zero{
  grid-column: 1/3
}

.btn{
  background-color: #F2F2F2;
  border: 1px solid #999;
  height: auto !important;
}

.operator{
 background: orange;
 color: white;
}
</style>
