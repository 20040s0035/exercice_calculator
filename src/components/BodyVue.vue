<template>
    <div id="culculate" class="body">
        <div class="input_container">
            <input class="input" readonly v-model="formula" type="text">
            <button class="button" v-on:click="clearAll()">C</button>
        </div>
        <div v-for="row in dataArrays" v-bind:key="row.id">
            <button class="button" v-for="column in row" v-bind:key="column.id"
                v-on:click="selectedNumber($event, column)">
                {{ column }}
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            el: '#calculate',
            formula: "0",
            number: 0,
            dataArrays: [
                [7, 8, 9, "÷"],
                [4, 5, 6, "×"],
                [1, 2, 3, "-"],
                [0, ".", "=", "+"],
            ],
            operations: ["÷", "×", "-", "+"],
        }
    },
    methods: {
        selectedNumber: function ($event, val) {
            //1. "=" の時
            if (val == "=") {
                this.formula = this.calculate;
            //2. "÷, ×, -, +" の時
            } else if (this.operations.includes(val) == true) {
                if (this.operations.some(c => c === this.formula.slice(-1)) == true) {
                    this.formula = this.formula.slice(0, -1);
                    this.addContext($event);
                } else if (this.formula.slice(-1) == "."){
                    this.formula = this.formula.slice(0, -1);
                    this.addContext($event);
                } else {
                    this.addContext($event);
                }
            //3. "." の時
            }else if (val == "."){
                if (this.operations.some(c => c === this.formula.slice(-1)) == true) {
                    this.formula += "0";
                    this.addContext($event);
                } else if (this.formula.slice(-1) == "."){
                    this.formula = this.formula.slice(0, -1);
                    this.addContext($event);
                } else {
                    this.addContext($event);
                }
            //4. "0" の時
            }else if (val == "0"){
            //5. 1,2,3,4,5,6,7,8,9 の時
            } else {
                if (this.formula == "0") {
                    this.formula = "";
                } else if (this.formula.slice(-1) == 0 && this.formula.slice(-2, -1).isNaN() == true) {
                    this.formula = this.formula.slice(0, -1);
                }
                this.addContext($event);
            }
            console.log(this.formula);
        },
        extractNumber: function() {
            formula.indexOf(this.operations)
            this.number = this.formula;
        },
        addContext: function ($event) {
            this.formula += $event.target.textContent;
        },
        
        clearAll: function () {
            this.formula = "0";
        }
    },
    computed: {
        calculate: function () {
            var calculate = eval(this.formula.replaceAll("×", "*").replaceAll("÷", "/"));
            return calculate;
        }
    },
}
</script>
<style scoped>
.body {
    text-align: center;
    padding: 20px;
    margin-left: 50px;
    margin-right: 50px;
}

.button {
    width: 50px;
    height: 30px;
}

.input_container {
    margin: auto;
    width: 200px;
    height: 30px;
}

.input {
    text-align: left;
    width: 71%;
    height: 79%;
}
</style>