<template>
    <div id="score">
        <h1>Score: <span class="counter">{{ printValue }}</span></h1>
        <div>
            <button v-on:click="up">Up</button>
            <button v-on:click="down">Down</button>
            <button v-on:click="get">Get</button>
            <input v-model.number="newValue" type="number">
            <button v-on:click="set">Set</button>
            <button v-on:click="reset">Reset</button>
            <button class="delete" v-on:click="selfDestroy">Delete</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'score',
        data () {
            return {
                maxValue: Math.pow(10, this.format) - 1,
                currentValue: this.value,
                newValue: 0
            }
        },
        computed: {
            printValue(){
                return new Array(this.format - (this.currentValue + "").length + 1).join(0) + this.currentValue;
            }
        },
        props: ['format', 'value', 'id'],
        methods: {
            up(){
                if (this.currentValue < this.maxValue) {
                    this.currentValue += 1;
                }
                else {
                    alert("Out of range");
                }
            },
            down(){
                if (this.currentValue > 0) {
                    this.currentValue -= 1;
                }
                else {
                    alert("Out of range");
                }
            },
            get(){
                alert(this.currentValue);
            },
            set(){
                if (this.newValue >= 0 && this.newValue <= this.maxValue) {
                    this.currentValue = this.newValue;
                }
                else {
                    alert("Out of range");
                }
            },
            reset(){
                this.currentValue = 0;
            },
            selfDestroy(){
                this.$emit("remove", this.id);
            }
        }
    }
</script>

<style>
    #score {
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

    .delete {
        background-color: #b92c28;
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

    .animatedCounter {
        -webkit-animation: counterAnim .5s linear;
        -moz-animation: counterAnim .5s linear;
        animation: counterAnim .5s linear;
        animation-fill-mode: forwards;
    }

    @-webkit-keyframes counterAnim {
        0% {
            -webkit-transform: translateY(-25%);
            opacity: 0
        }
        100% {
            -webkit-transform: translateY(0);
            opacity: 1
        }
    }

    @-moz-keyframes counterAnim {
        0% {
            -moz-transform: translateY(-25%);
            opacity: 0
        }
        100% {
            -moz-transform: translateY(0);
            opacity: 1
        }
    }

    @keyframes counterAnim {
        0% {
            transform: translateY(-25%);
            opacity: 0
        }
        100% {
            transform: translateY(0);
            opacity: 1
        }
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
