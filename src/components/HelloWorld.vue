
<!-- Adnan Akram 

  Title: Front End 

-->

<template>
  <div class="calculator">
    <div class="dis"> {{ cur || '0'}}</div>
    <div @click="clear" class="btns">C</div>
    <div @click="sinmethod"  class="btns">+/-</div>
    <div @click="perage" class="btns" > %</div>
    <div @click="divd" class="btns oper"> ÷</div>
    <div @click="append('7')" class="btns">7</div>
    <div @click="append('8')" class="btns">8</div>
    <div @click="append('9')" class="btns">9</div>
    <div @click="mul" class="btns oper" >x</div>
    <div @click="append('4')" class="btns">4</div>
    <div @click="append('5')" class="btns">5</div>
    <div @click="append('6')" class="btns">6</div>
    <div @click="slice" class="btns oper">-</div>
    <div @click="append('1')" class="btns">1</div>
    <div @click="append('2')" class="btns">2</div>
    <div @click="append('3')" class="btns">3</div>
    <div @click="plus" class="btns oper">+</div>
    <div @click="append('0')" class="zer btns">0</div>
    <div @click=dot class="btns">.</div>
    <div @click="equal"  class="btns oper">=</div>
    
  
  </div>
</template>

<script>
export default {
  data()
  {
    return{
      perv:null,
      cur: '',
      operter:null,
      operterClick:false,
    }
  },
  methods:{
    clear(){
      this.cur = ''
    },
    sinmethod(){
      this.cur = this.cur.charAt(0)=='-' ?
      this.cur.slice(1):`-${this.cur}`;
    },
    perage(){
      this.cur=`${parseFloat(this.cur)/100}`;
      
    },
    append(num){
      if(this.operterClick){
        this.cur = '';
        this.operterClick = false;
      }
      this.cur=`${this.cur}${num}`;
      
    },
    dot(){
        if(this.cur.indexOf('.')===-1){
          this.append('.')

        }
    },
    setPrev(){
      this.perv = this.cur;
        this.operterClick=true;
        

    },
    divd(){
        this.operter = (a,b)=>a / b;
        this.setPrev()
      
    
    },
    mul(){
      this.operter = (a,b)=>a*b;
      this.setPrev()
      

    },
    slice(){
      this.operter = (a,b)=>b-a;
      this.setPrev(true)
      
    },
    plus(){
      this.operter = (a,b)=>a+b;
      this.setPrev()
      

    },
    equal(){
        this.cur=`${this.operter(
            parseFloat(this.cur),
             parseFloat(this.perv))}`;
             this.perv = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto );
  width: 20rem;
  margin: 0 auto;
  font-size: 40px;
}
.dis{
  grid-column: 1/5;
  background-color:#333;
  color: #eee;
  text-align: center;
  padding-top: 1rem;
}
.zer{
  grid-column: 1/3;
  /* text-align:; */
  /* margin-left: 100px; */
}
.btns{
  background-color:#eee ;
  border: 1px solid #333;
  text-align: center;
}
.oper{
  background-color:orangered;
  color: white ;

}
</style>
