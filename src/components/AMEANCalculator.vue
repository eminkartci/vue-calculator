<template>
  
  <!-- CALCULATOR -->
  <div class="p-3 calculator_main">
     
    <!-- RESULT -->
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorValue || 0}}
    </div>

    <!-- BUTTONS -->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class" 
        :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}" 
        @click="action(n)">
          {{ n }}
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line
  name: 'Calculator',
  props: {
    msg: String
  },

  data() {
    return {
      calculatorValue: '',
      calculatorElements: ["C","*","/","-","7","8","9","+","4","5","6","%","1","2","3","=","0","."],
      operator: null,
      prevCalcValue: ''
    }
  },

  methods:{
    action(n){

      /* Append the Value*/
      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }

      /* Clear Option*/
      if(n === 'C'){
        this.calculatorValue = '';
      }

      /* % Option */
      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }

      /* Operations */
      if(['*','/','-','+'].includes(n)){
        this.operator = n;
        this.prevCalcValue = this.calculatorValue
        this.calculatorValue = ''
      }

      /* Calculate Result */
      if(n === '='){
        this.calculatorValue = eval(
          this.prevCalcValue + this.operator + this.calculatorValue
        )

        this.prevCalcValue = '';
        this.operator = null
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator_main{
    max-width: 400px;
    margin: 50px auto;
    background: #234;

  }
  .bg-vue-dark{
    background: #31475e;
    text-align: right;
  }
  .bg-vue-green{
    background: #3fb984;
  }
  .hover-class:hover{
    cursor: pointer;
    background: #3D5875;
  }
</style>
