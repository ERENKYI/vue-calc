<template>
    <div class="calculator-button" @click="buttonClick">{{buttons[val-1]}}</div>
</template>

<script>
    export default {
        name: "CalculatorButton",
        props: {
            val: Number
        },
        data: function () {
            return {
                buttons: ["AC", "+/-", "%", "÷",
                    "7", "8", "9", "x",
                    "4", "5", "6", "-",
                    "1", "2", "3", "+",
                    "", "0", ".", "="]
            }
        },
        methods: {
            buttonClick: function () {
                this.$emit('buttonClick', this.buttons[this.val - 1]);
            }
        }
    }
</script>

<style>
    .calculator-button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 75px;
        height: 70px;
        background: #8C9196;
        box-shadow: 0 0 0 1px #9EA2A7;
        cursor: pointer;
        -webkit-transition: background .1s;
        -moz-transition: background .1s;
        -ms-transition: background .1s;
        -o-transition: background .1s;
        transition: background .1s;
    }

    .calculator-button:hover {
        background: #999ea3;
    }

    .calculator-button:nth-child(4n) {
        background: #fff;
        color: #495565;
        box-shadow: 0 0 0 1px #DDDDDD, 0 14px 18px 6px rgba(0, 0, 0, .14)
    }

    .calculator-button:nth-child(4n):hover {
        background: #f0f0f0;
    }

    .calculator-button:last-child {
        background: #FF303D;
        color: #fff;
        box-shadow: 0 0 0 1px #ff0a1b, 0 14px 18px 6px rgba(0, 0, 0, .14)
    }

    .calculator-button:last-child:hover {
        background: #ff4d58;
    }
</style>