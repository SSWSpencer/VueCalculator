<template>
    <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">

        <div class="w-full rounded m-1 p-3 lead text-white bg-vue-dark" style="font-weight: bold; text-align: right">
            {{ calculatorValue || 0 }}
        </div>

        <div class="row" style="padding-left: 3%; padding-right: 3%;">
            <div class="col-3 p-0" v-for="n in calculatorElements" :key=n>
                <div class="lead text-white text-center py-3 m-1 bg-vue-dark rounded hover-class" :class="{'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n)}" @click="action(n)">
                    {{ n }}
                </div>
            </div>
        </div>
    </div>

</template>


<script>
export default{
    name: "Calculator",

    data() {
    return{
        calculatorValue: "",
        calculatorElements: ['C', '*', '/', '-', 7, 8, 9, "+", 4, 5, 6, '%', 1, 2, 3, '=', 0, '.'],
        operator: null,
        previousCalculatorValue: ""
    }
},

methods: {
    action(n){
        if(!isNaN(n) || n === '.'){
            this.calculatorValue += n + '';
        }

        if(n === "C"){
            this.calculatorValue = '';
        }

        if(n === "%"){
            this.calculatorValue = this.calculatorValue / 100 + '';
        }

        if(['*', '/', '+', '-'].includes(n)){
            if(!this.previousCalculatorValue){
                this.operator = n;
                this.previousCalculatorValue = this.calculatorValue;
                this.calculatorValue = "";
            }
            else{
                this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue);
                this.operator = n;
                this.previousCalculatorValue = this.calculatorValue;
                this.calculatorValue = "";
            }
        }

        if(n === "="){
            this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue);
            this.previousCalculatorValue = "";
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
.hover-class:hover{
    cursor: pointer;
    background: #3D5875;

}
.bg-vue-green{
    background: #3fb984;
}

</style>