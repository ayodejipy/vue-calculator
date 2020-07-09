<template>
    <div class="calculator-wrap">
        <div class="result-input">
            <span> {{ result || '0'}} </span>
        </div>

        <div class="calculator-buttons">
            <div class="row">
                <div class="col">
                    <button class="calculator-btn gray action" @click="clear()">AC</button>
                </div>
                <div class="col">
                    <button class="calculator-btn gray action" @click="addSign()">+/-</button>
                </div>
                <div class="col">
                    <button class="calculator-btn gray action" @click="percent()">%</button>
                </div>
                <div class="col">
                    <button class="calculator-btn accent action" @click="divide()">&#xf7;</button>
                </div>
            </div>
            <div class="row">
                <div class="col">
                <button class="calculator-btn" @click="append('7')">7</button>
                </div>
                <div class="col">
                <button class="calculator-btn" @click="append('8')">8</button>
                </div>
                <div class="col">
                <button class="calculator-btn" @click="append('9')">9</button>
                </div>
                <div class="col">
                <button class="calculator-btn accent action" @click="multiply()">&#xd7;</button>
                </div>
            </div>
            <div class="row">
                <div class="col">
                <button class="calculator-btn" @click="append('4')">4</button>
                </div>
                <div class="col">
                    <button class="calculator-btn" @click="append('5')">5</button>
                </div>
                <div class="col">
                    <button class="calculator-btn" @click="append('6')">6</button>
                </div>
                <div class="col">
                    <button class="calculator-btn accent action" @click="subtract()">-</button>
                </div>
            </div>
            <div class="row">
                <div class="col">
                <button class="calculator-btn" @click="append('1')">1</button>
                </div>
                <div class="col">
                <button class="calculator-btn" @click="append('2')">2</button>
                </div>
                <div class="col">
                <button class="calculator-btn" @click="append('3')">3</button>
                </div>
                <div class="col">
                <button class="calculator-btn accent action" @click="plus()">+</button>
                </div>
            </div>
            <div class="row">
                <div class="col wide">
                <button class="calculator-btn zero" @click="append('0')">0</button>
                </div>
                <div class="col">
                <button class="calculator-btn action" @click="dot()">.</button>
                </div>
                <div class="col">
                <button class="calculator-btn accent action" @click="getResult()">=</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
        prevResult: null,
        result: '',
        operator: null,
        clickedOperator: false

    }
  },
  methods: {
    append(number) {
        // If true, set current value to false
        if (this.clickedOperator) {
            this.result = '';
            this.clickedOperator = false
        }
        this.result = `${this.result}${number}`;
        // this.result = this.result + number;
    },
    clear() {
        this.result = "";
    },
    addSign() {
        this.result = this.result.charAt(0) === '-' ? this.result.slice(1) : `-${this.result}`;
    },
    percent() {
        // convert this.result from string to float then divide by 100
        // and casted back to string with string literal
        this.result = `${parseFloat(this.result) / 100}`;
    },
    dot() {
        if (this.result.indexOf('.') === -1) {
            this.append('.');
        }
        // this.result.indexOf('.') === -1 ?? this.append('.');
    },
    setPrevious() {
        // set the current result/value as the prev
        this.prevResult = this.result;
        this.clickedOperator = true
    },
    plus() {
        // takes a callback function that perform function's operation
        this.operator = (a, b) => a + b;
        this.setPrevious();
    },
    subtract() {
        // takes a callback function that perform function's operation
        this.operator = (a, b) => a - b;
        this.setPrevious();
    },
    divide() {
        // takes a callback function that perform function's operation
        this.operator = (a, b) => a / b;
        this.setPrevious();
    },
    multiply() {
        // takes a callback function that perform function's operation
        this.operator = (a, b) => a * b;
        this.setPrevious();
    },
    getResult() {
        // this.operator callback function takes parameters
        this.result = `${this.operator(
            parseFloat(this.prevResult),
            parseFloat(this.result)
        )}`;
        this.prevResult = null;
    }
  }
}
</script>

<style>
:root {
    --darker: #2f2f31;
    --dark: #424345;
    --gray: #616163;
    --white: #fff;
    --light: #D4D4D2;
    --accent: #f49e3f;
}

.calculator-wrap {
    width: 100%;
    margin: 0 auto;
    display: flex;
    padding: 0;
    max-width: 320px;
    min-width: 320px;
    flex-direction: column;
    background-color: var(--darker);
}
.result-input {
    color: var(--light);
    width: 90%;
    border: none;
    padding: .8rem;
    display: block;
    font-size: 2.4rem;
    background: none;
    text-align: right;
    font-weight: lighter;
}
.result-input:focus, 
.result-input:active {
    outline: none;
}

.row {
    display: flex;
    padding: 0;
    justify-content: space-around;
}
.col {
    flex: 1;
}

.col.wide { 
    flex: 2; 
}

.calculator-btn {
    width: 60px;
    height: 60px;
    color: #D4D4D2;;
    border: none;
    cursor: pointer;
    padding: .8rem;
    margin: .3rem 0;
    outline: none;
    font-size: 1.6rem;
    transition: all .3s ease-in-out;
    font-weight: 200;
    justify-content: center;
    background-color: #424345;
    border-radius: 30px;
}

.zero {
    width: 90%;
    text-align: start;
    border-radius: 30px;
}

.calculator-btn.accent { 
    background-color: var(--accent); 
    color: var(--white); 
}

.calculator-btn.gray { 
    background-color: var(--gray); 
}
.calculator-btn:active {
    background-color: #2f2f31;;
}


</style>
