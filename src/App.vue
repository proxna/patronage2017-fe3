<template>
    <div id="app">
        <div class="head">
            <div>
                <label for="format">Format</label>
                <input v-model.number="newCountFormat" name="format" type="number">
                <label for="value">Value</label>
                <input v-model.number="newCountValue" name="value" type="number">
            </div>
            <button v-on:click="addCounter()">Add Counter</button>
            <button v-on:click="removeLast()">Remove Last Counter</button>
        </div>
        <counter v-for="counter in counters" :format="counter.format" :value="counter.value" :id="counter.id" v-on:remove="remove" :key="id"></counter>
    </div>
</template>

<script>
    import Counter from './components/counter.vue'

    export default {
        name: 'app',
        data () {
            return {
                id: 0,
                newCountValue: 0,
                newCountFormat: 0,
                counters: []
            }
        },
        components: {
            "counter": Counter
        },
        methods: {
            addCounter(){
                console.log();
                if (this.newCountValue >= 0 && this.newCountValue <= Math.pow(10, this.newCountFormat) - 1) {
                    var newCounter = {
                        format: this.newCountFormat,
                        value: this.newCountValue,
                        id: this.id
                    };
                    ++this.id;
                    this.counters.push(newCounter);
                }
                else {
                    alert("value out of range")
                }
            },
            removeLast(){
                this.counters.pop();
            },
            remove(id){
                this.counters = this.counters.filter(el => {
                            return el.id !== id;
                });
            }
        }
    }
</script>

<style>
    .head {
        display: flex;
        justify-content: center;
        width: 90%;
        padding: 2em;
        border: 2px solid #bfbfbf;
        margin: 2em auto;
        -webkit-box-shadow: 1px 1px 2px 0 rgba(237, 237, 237, 1);
        -moz-box-shadow: 1px 1px 2px 0 rgba(237, 237, 237, 1);
        box-shadow: 1px 1px 2px 0 rgba(237, 237, 237, 1)
    }

    button {
        background-color: #ff4d00;
        color: #fff;
        border: none;
        min-width: 8em;
        height: 3em;
        margin: 0.5em 1em;
        -webkit-transition: .25s ease;
        -moz-transition: .25s ease;
        transition: .25s ease;
        -webkit-box-shadow: 1px 1px 2px 0 rgba(158, 158, 158, 1);
        -moz-box-shadow: 1px 1px 2px 0 rgba(158, 158, 158, 1);
        box-shadow: 1px 1px 2px 0 rgba(158, 158, 158, 1)
    }

    button:hover {
        -webkit-transform: scale(1.1);
        -moz-transform: scale(1.1);
        transform: scale(1.1);
    }

    button:active {
        -webkit-transform: scale(.9);
        -moz-transform: scale(.9);
        transform: scale(.9);
    }

    input {
        height: 2.5em;
        margin-top: 1%;
        border-color: #bababa;
        border-radius: 5px;
        border-style: solid
    }

    input:hover {
        -webkit-animation: fadeShadow .2s linear;
        -moz-animation: fadeShadow .2s linear;
        animation: fadeShadow .2s linear;
        animation-fill-mode: forwards;
    }

    @-webkit-keyframes fadeShadow {
        0% {
            -webkit-box-shadow: none
        }
        100% {
            -webkit-box-shadow: 0 0 20px 5px rgba(231, 166, 26, 1)
        }
    }

    @-moz-keyframes fadeShadow {
        0% {
            -moz-box-shadow: none
        }
        100% {
            -moz-box-shadow: 0 0 20px 5px rgba(231, 166, 26, 1)
        }
    }

    @keyframes fadeShadow {
        0% {
            box-shadow: none
        }
        100% {
            box-shadow: 0 0 20px 5px rgba(231, 166, 26, 1)
        }
    }
</style>
