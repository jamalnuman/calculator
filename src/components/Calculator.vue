<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div @click='clear()' class="btn">C</div>
    <div @click='sign()' class="btn">+/-</div>
    <div @click='percent()' class="btn">%</div>
    <div @click='divide()' class="operator btn">÷</div>
    <div @click='append("7")' class="btn">7</div>
    <div @click='append("8")' class="btn">8</div>
    <div @click='append("9")' class="btn">9</div>
    <div @click='times()' class="operator btn">x</div>
    <div @click='append("4")' class="btn">4</div>
    <div @click='append("5")' class="btn">5</div>
    <div @click='append("6")' class="btn">6</div>
    <div @click='subtract()' class="operator btn">-</div>
    <div @click='append("1")' class="btn">1</div>
    <div @click='append("2")' class="btn">2</div>
    <div @click='append("3")' class="btn">3</div>
    <div @click= 'addition()' class="operator btn">+</div>
    <div @click='append("0")' class="zero btn">0</div>
    <div @click='dot()' class="btn">.</div>
    <div @click= 'total()' class="operator btn">=</div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        current: "",
        operator: null,
        previous: null,
        operatorClicked: false
      }
    },
    methods:{
      append: function(val) {
        if (this.operatorClicked) {
          this.current = ""
          this.operatorClicked = false
        }
        if(this.current.length < 15) {
          this.current += val  
        }
        
      },

      clear: function() {
        this.current = ""
      },

      sign: function() {
        this.current = this.current.charAt(0) === "-" ? this.current.slice(1) : `-${this.current}`
      },

      percent: function() {
        this.current = parseFloat(this.current) / 100
      },

      dot: function() {
        if (this.current.indexOf('.') === -1) {
          this.append('.')
        }
      },

      setPrevious: function() {
        this.previous = this.current;
        this.operatorClicked = true
      },

      divide() {
        this.operator = (a, b) => a / b
        this.setPrevious()
      },

      times() { 
        this.operator = (a, b) => a * b
        this.setPrevious()
      },

      subtract() {
        this.operator = (a, b) => a - b
        this.setPrevious()
      },

      addition() {
        this.operator = (a, b) => a + b
        this.setPrevious()
      },

      total() {
        this.current = this.operator(parseFloat(this.previous), parseFloat(this.current));
        this.previous = null
      }
    }
  }
</script>


<style scoped>
.calculator {
  width: 400px;
  /*letter-spacing: 10px;*/
  margin: 0 auto; /*centers the calculator on the screen*/
  font-size: 40px;
  display: grid; /*without 'grid' the caluclator would be in a line up/down*/
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: (50px, auto); 
} 
.display {
  grid-column: 1 / 5;
  
} 
.zero {
  grid-column: 1/3;
}  

.btn {
  background-color: #eee;
  border: 1px solid #333; /*provides each button the 'box-like look'*/
  cursor: pointer
}
.operator {
  background-color: orange;
  color: white;
}
</style>





