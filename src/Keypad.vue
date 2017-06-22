<template>
    <div class="buttons">
        <div class="row">
            <div @click="optionPressed('clear')" class="key grey" id="clear">AC</div>
            <div @click="operatorPressed('toggleSign')" class="key grey" id="toggleSign">
                <span><sup>+</sup>/<sub class="minus">-</sub></span>
            </div>
            <div @click="operatorPressed('percentage')" class="key grey" id="percentage">%</div>
            <div @click="operatorPressed('divide')" class="key orange operator">/</div>
        </div>
        <div class="row">
            <div @click="keyPressed(7)" class="key num">7</div>
            <div @click="keyPressed(8)" class="key num">8</div>
            <div @click="keyPressed(9)" class="key num">9</div>
            <div @click="operatorPressed('multiply')" class="key orange operator">*</div>
        </div>
        <div class="row">
            <div @click="keyPressed(4)" class="key num">4</div>
            <div @click="keyPressed(5)" class="key num">5</div>
            <div @click="keyPressed(6)" class="key num">6</div>
            <div @click="operatorPressed('substract')" class="key orange operator">-</div>
        </div>
        <div class="row">
            <div @click="keyPressed(1)" class="key num">1</div>
            <div @click="keyPressed(2)" class="key num">2</div>
            <div @click="keyPressed(3)" class="key num">3</div>
            <div @click="operatorPressed('add')" class="key orange operator">+</div>
        </div>
        <div class="row">
            <div @click="keyPressed(0)" class="key num wide">0</div>
            <div @click="keyPressed('.')" class="key num">.</div>
            <div @click="optionPressed('equal')" class="key orange equal" id="equal">=</div>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'keypad',

    data () {
      return {
      }
    },

    methods: {
      keyPressed (key) {
        this.$emit('keyPressed', key)
      },

      optionPressed (option) {
        this.$emit(option)
      },

      operatorPressed(option) {
        this.optionPressed(option)
      }
    }
  }
</script>

<style lang="scss">
    .keypad {
        .numerics {
            display: flex;
            flex-wrap: wrap;
            width: 100%;
        }
        .functions {
            float: left;
            width: 30px;
        }

        .button {
            flex: 0 1 25%;
            font-size: 36px;
            cursor: pointer;
            background-color: white;
            border: none;

            &:hover {
                background-color: #EEEEEE;
            }

            &.zero-btn{
                flex-grow: 2;
            }
        }
    }
</style>
