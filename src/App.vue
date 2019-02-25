<template>
    <div id="app">
        <Calculator/>
    </div>
</template>

<script>
    import Calculator from './components/Calculator'

    export default {
        name: 'app',
        components: {
            Calculator
        }
    }
</script>

<style>
    html, body {
        height: 100%;
    }

    body {
        background: #a2afbe;
        margin: 0;
    }

    #app {
        font-family: 'Roboto', Helvetica, Arial, sans-serif;
        font-weight: 300;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: white;
        text-align: center;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
