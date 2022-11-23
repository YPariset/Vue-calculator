<template>
  <div class= "p-3" style= "max-width: 400px; margin: 50px auto; background: #234">
    <div class= "w-full rounded m-1 p-3 input bg-vue-dark">
      {{ calculatorValue || 0 }}
    </div>
    <div class= "row no-gutters">
      <div class= "col-3" v-for="n in calculatorElements" :key="n">
        <div class= "lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class= "{'bg-vue-button': ['C','%','/','*','-','+','='].includes(n)}"
          @click="action(n)">
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C','%','/','*',1,2,3,'-',4,5,6,'+',7,8,9,'=',0,'.'],
      operator: null,
      previousCalculatorValue: '',
    }
  },
  methods: {
    action(n){
      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }
      if(n === 'C'){
        this.calculatorValue = '';
      }
      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }
      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }
      if(n === '='){
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    }
  }
}
</script>


<style scoped>
  .bg-vue-dark {
    background: #31475e;
  }
  .hover-class:hover {
    cursor: pointer;
    background: #3D5875;
  }
  .bg-vue-button {
     background-color: rgb(80, 60, 209);
  }
  .bg-vue-button:hover {
     background-color: rgb(61, 43, 184);
  }
   .input {
     color: white;
     font-weight: bold;
     width: 100%;
  }
</style>