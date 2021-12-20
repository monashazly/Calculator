<template>
<!-- calculator Display -->
  <div class="p-3 rounded" style="max-width:350px ;background:#234;margin: 50px auto" >
    <div class="m-1 p-3 rounded w-full lead text-white display ">{{calculatorValue ||0}}</div>
<!-- calculator buttons -->
      <div class="row no-gutters ">
        <div class="col-3 shadow" v-for="element in Elements" :key="element">
          <div class="lead text-white text-center mt-1 mb-1 p-3 bg-vue-dark rounded hover-class" :class="{'greenColor':['c','*','/','-','=','%','+'].includes(element)}"
          @click="action(element)"
          >
            {{element}}
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
  data(){
    return{
      calculatorValue:'',
      Elements:['c','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      Prevalue:'',
      operator:null

    }
  },
  methods:{
    action(element){
      if(!isNaN(element)||element==='.'){
        this.calculatorValue +=element +'';
      }

      if(element==='c'){
        this.calculatorValue='';
      }
      if(element==='%'){
        this.calculatorValue=this.calculatorValue/100 +'';
      }
      if(['/','*','-','+'].includes(element)){
         this.operator=element;
         this.Prevalue=this.calculatorValue;
         this.calculatorValue='';
      }
      if(element==='='){
        this.calculatorValue=eval(
          this.Prevalue + this.operator+this.calculatorValue
        )
        
      }
    }
  }
}
</script>


<style scoped>
.display{
  background:#31475e;
  text-align: right;
}
.bg-vue-dark{
  background: #31475e;
 
}
.hover-class:hover{
  cursor: pointer;
  animation:tada;
  animation-duration: 2s;
  background: #3D5875;
}
.greenColor{
  background: #3fb984;
}
</style>
