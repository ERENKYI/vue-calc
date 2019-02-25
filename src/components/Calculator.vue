<template>
    <div class="calculator" :class="{_80085: easter}">
        <div class="calculator-header">
            <div class="operation">{{operation}}</div>
            <div class="input">{{input}}</div>
        </div>
        <div class="calculator-buttons">
            <CalculatorButton v-for="i in 20" :val="i" v-on:buttonClick="buttonClick"></CalculatorButton>
        </div>
    </div>
</template>

<script>
    import CalculatorButton from "@/components/CalculatorButton";

    window.x = require('expr-eval').Parser;
    let parser = new window.x();

    export default {
        name: "Calculator",
        components: {CalculatorButton},
        data: function () {
            return {
                input: '0',
                operation: '0',
                afterCalculation: false,
                afterError: false,
                easter: false
            }
        },
        computed: {},
        methods: {
            buttonClick: function (button) {
                if (this.afterError) {
                    this.input = "0";
                    this.afterError = false;
                }

                if (button === 'AC') {
                    this.input = "0";
                    this.operation = "0";
                } else if (button === '+/-') {
                    // Convert - to + and vice versa. No plus or minus signs means it's plus :)
                    if (this.input.startsWith("-")) {
                        this.input = this.input.substr(1);
                    } else {
                        this.input = "-" + this.input;
                    }
                } else if (button === '÷' || button === 'x' || button === '+' || button === '-' || button == '%') {
                    this.operation = this.input + button;
                    this.input = "0";
                } else if (button === '=') {
                    this.operation = this.operation + this.input + button;
                    try {
                        this.input = parser.evaluate(this.operation.substr(0, this.operation.length - 1).replace(/x/g, "*").replace(/÷/g, "/"));
                    } catch (e) {
                        console.error("An error happened while trying to calculate. " + e);
                        this.input = "ERROR";
                        this.operation = "0";
                        this.afterError = true;
                    }
                    this.afterCalculation = true;
                } else if (button === '') {
                    if (this.input === "80085") this.easter = true
                } else { // Most likely a number or dot sign unless values edited.
                    // If the calculator has been cleaned (input=0 or input=-0) change the 0 to the number pressed.
                    // If the condition is met but the button is '.', it will behave like there is a
                    // number entered (which is 0).
                    if ((this.input === "0" && button !== ".") || (this.input === "-0" && button !== ".")) {
                        if (this.input.startsWith("-")) {
                            this.input = "-" + button;
                        } else {
                            this.input = button;
                        }
                    } else {
                        if (this.afterCalculation) {
                            this.operation = "0";
                            this.input = button
                        } else {
                            this.input += button;
                        }
                    }

                    if (this.afterCalculation) {
                        this.afterCalculation = false;
                    }
                }
            }
        }
    }
</script>

<style>
    .calculator {
        width: 300px;
        background: #5b6269;
        -webkit-border-radius: 20px;
        -moz-border-radius: 20px;
        border-radius: 20px;
        padding: 0;
        overflow: hidden;
        box-shadow: 0 0 18px 6px rgba(0, 0, 0, .15);
    }

    .calculator._80085 {
        font-family: 'Orbitron', 'Roboto', Helvetica, Arial, sans-serif !important;
    }

    .operation {
        font-size: 14px;
        background: #474e55;
        padding: 6px;
    }

    .input {
        font-size: 24px;
        padding: 24px 12px;
    }

    .operation, .input {
        color: white;
        text-align: right;
        padding-right: 30px;
    }

    .calculator-buttons {
        display: flex;
        flex-wrap: wrap;
        max-width: 300px;
        user-select: none;
        -webkit-user-select: none;
        -ms-user-select: none;
        -webkit-touch-callout: none;
        -o-user-select: none;
        -moz-user-select: none;
    }

</style>