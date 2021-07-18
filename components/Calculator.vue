<template>
  <div class="section">
        <div class="calculator">
            <div class="display" id="numDisplay">{{currNum || '0'}}</div>
            <button class="btn" @click="AppendNumber('7')">7</button>
            <button class="btn" @click="AppendNumber('8')">8</button>
            <button class="btn" @click="AppendNumber('9')">9</button>
            <button class="btn operationBtn" @click="GetOperator('/')">÷</button>
            <button class="btn" @click="AppendNumber('4')">4</button>
            <button class="btn" @click="AppendNumber('5')">5</button>
            <button class="btn" @click="AppendNumber('6')">6</button>
            <button class="btn operationBtn" @click="GetOperator('*')">x</button>
            <button class="btn" @click="AppendNumber('1')">1</button>
            <button class="btn" @click="AppendNumber('2')">2</button>
            <button class="btn" @click="AppendNumber('3')">3</button>
            <button class="btn operationBtn" @click="GetOperator('-')">-</button>
            <button class="btn delBtn" @click="DeleteNumber()">Del</button>
            <button class="btn" @click="AppendNumber('0')">0</button>
            <button class="btn" @click="SetDotOnNumber()">.</button>
            <button class="btn operationBtn" @click="GetOperator('+')">+</button>
            <button class="btn cancelBtn" @click="ClearNumber()">C</button>
            <button class="btn equalBtn" @click="Calculate()">=</button>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
        previousNum:'',
        currNum:'',
        operator: '',
        isOperatorBtnPress: false
    }
  },
  methods:{
      //Delte number
    DeleteNumber(){
      this.currNum = this.currNum.slice(0, this.currNum.length-1);
    },
    //Clear number
    ClearNumber(){
      this.currNum = '';
    },
    //put a peroid sign into numbers
    SetDotOnNumber(){
        if(!this.currNum.includes('.')){
            this.currNum = `${this.currNum}${'.'}`;
        }
    },
    AppendNumber(n){
        if(this.isOperatorBtnPress){
            this.currNum = '';
            this.isOperatorBtnPress = false;
        }
        this.currNum = `${this.currNum}${n}`;
    },
    GetOperator(op){
        this.operator = op;
        this.previousNum = this.currNum;
        this.isOperatorBtnPress = true;
    },
    Calculate(){
        var tempCurrNum = this.currNum;
        switch(this.operator){
            case '+':{
                this.currNum = (parseFloat(this.previousNum) + parseFloat(tempCurrNum)).toString();
            }break;
            case '-':{
                this.currNum = (parseFloat(this.previousNum) - parseFloat(tempCurrNum)).toString();
            }break;
            case '*':{
                this.currNum = (parseFloat(this.previousNum) * parseFloat(tempCurrNum)).toString();
            }break;
            case '/':{
                this.currNum = (parseFloat(this.previousNum) / parseFloat(tempCurrNum)).toString();
            }break;
            default: {
                this.currNum = "invalid";
            }break;
        }
        this.previousNum = '';
        this.operator = '';
    }
  }
}
</script>