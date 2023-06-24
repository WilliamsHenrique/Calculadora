
<script>
import { getCurrentInstance } from 'vue';

export default {
  name: 'Calculator',
  props: {
    msg: String
  },

  data() {
    return {
      calcValor: '',
      calcNum: ['C', '%', '=', '+', 7, 8, 9,'-', 4, 5, 6,'*', 1, 2, 3, '/', 0, '.'],
      operadores: null,
      prevcalcValor: ''
    }
  }, 
  methods: {
    action(btn){

      if(!isNaN(btn) || btn === '.')
      {
        this.calcValor += btn +''
      }

      if (btn === 'C') {
        this.calcValor = ''
      }

      if (btn === '%') {
        this.calcValor = this.calcValor / 100 + ''
      }

      if (['/', '+', '-', '*'].includes(btn)) {
        this.operadores = btn
        this.prevcalcValor = this.calcValor
        this.calcValor = ''
      }

      if (btn === "=") {
          this.calcValor = eval(
            this.prevcalcValor + this.operadores + this.calcValor
            )
          this.prevcalcValor = ''
          this.operadores = null
      }
    }
  },
}
</script>



<template>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background-color: #234;">

    <div class="w-full rounded m-1 p-3 text-end lead fw-bold text-white digitos">
      {{ calcValor || 0}}
    </div>  

    <div class="row g-0">
      <div class="col-3" v-for="btn in calcNum">
        <div 
        class="lead text-white text-center m-1 py-3 digitos rounded resultado"
        :class="{'operadores': ['C', '*', '/', '+', '-', '=', '%'].includes(btn)}"
        @click="action(btn)"
          >
          {{ btn }}
        </div>
      </div>
    </div>
  </div>    
</template>


<style scoped>
.digitos{
  background: rgba(23, 84, 134, 0.5);
  backdrop-filter: blur(10px);
  max-width: 350px;
  margin: 50px auto 0;
  border-radius: 20px;
  box-shadow: 0 10px 30px 1px rgba(0,0,0,.5);
  overflow: hidden; 
}

.resultado:hover{
  cursor: pointer;
  background: #4490e2;
}

.operadores{
  background: #3fb984 ;
}
</style>
