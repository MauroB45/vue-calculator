<template>
    <div class="calculator active" id="calculator">
        <div class="controls">
            <span class="red"   id="close"></span>
            <span class="amber" id="minimise"></span>
            <span class="green" id="maximise"></span>
        </div>

        <div class="frame">
            <div class="screen" id="screen">
                <div class="text" id="text"><div class="result" id="result">{{display}}</div></div>
                <div class="label" id="label">OS X Calculator</div>
            </div>
            <keypad @keyPressed="keyPressed"
                    @clear="clear"></keypad>
        </div>
    </div>
</template>

<script>
  import Keypad from './Keypad.vue'

  export default {
    name: 'calculator',
    data () {
      return {
        display: "",
        number: 2
      }
    },

    components: {
      Keypad
    },

    methods: {
      keyPressed(key) {
        this.display += key.toString()
      },

      clear(key) {
        this.display = ''
      }
    }
  }
</script>

<style lang="scss">
    $amber-500: #fdbb3c;
    $black-500: #333;
    $green-500: #39c847;
    $grey-300: #e4e4e4;
    $grey-500: #d5d5d5;
    $grey-700: #afafaf;
    $orange-500: #f68f24;
    $red-500: #fb5252;

    $minimised: 88px;

    *, *:before, *:after {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    html,
    body {
        overflow: hidden;
        height: 100%;
    }

    body {
        background: linear-gradient(180deg, #5494af, #eaa75a);
        font-family: "HelveticaNeue-UltraLight", "Helvetica Ultra Light", "Helvetica Neue", Helvetica, Arial, sans-serif;
        font-size: 1.25em;
    }

    .button {
        $width: 156px;
        background-color: rgba(#fff, .5);
        border-radius: 30px;
        bottom: 16px;
        box-shadow: 0 2px 4px rgba($black-500, .35);
        color: rgba($black-500, .5);
        cursor: pointer;
        display: flex;
        flex-direction: column;
        height: 64px;
        justify-content: center;
        left: calc(50% - #{$width / 2});
        position: absolute;
        text-align: center;
        transform: translateY(80px);
        width: $width;
        transition: transform .4s, box-shadow .4s, background-color .4s, color .4s;

        &:hover {
            background-color: rgba(#fff, .8);
            box-shadow: 0 5px 4px rgba($black-500, .35);
            color: rgba($black-500, 1);
            transform: translateY(-3px);
        }

        &.active {
            transform: translateY(0);
        }
    }

    .calculator {
        height: 80%;
        max-height: 640px;
        max-width: 480px;
        min-height: 320px;
        min-width: 240px;
        opacity: 0;
        position: relative;
        transform-origin: 50% 0;
        transform: scale(1.2);
        transition: opacity .4s, transform .4s cubic-bezier(.17, .67, .83, .67);
        margin: 2em;

        &.active {
            opacity: 1;
            transform: scale(1);
        }

        &.minimised {
            height: $minimised;

            > .frame {
                height: $minimised;

                > .buttons {
                    transform: scaleY(0);
                }

                > .screen {
                    height: 100%;

                    .result {
                        opacity: 0;
                    }

                    > .label {
                        opacity: 1;
                    }
                }
            }
        }

        > .frame {
            border-radius: 8px;
            box-shadow: 0 10px 30px #4e4e4e;
            height: 100%;
            overflow: hidden;
            transform: scale(1);
            transform-origin: 50% 0;
            width: 100%;
            transition: height .4s cubic-bezier(.17, .67, .54, .99);

            > .screen {
                background-color: rgba(#333333, .8);
                height: 27.5%;
                position: relative;
                transition: height .4s;

                .result,
                .label {
                    bottom: 0;
                    color: #fff;
                    display: flex;
                    flex-direction: column;
                    font-size: 3em;
                    justify-content: flex-end;
                    padding: 0 .35em .1em;
                    position: absolute;
                    right: 0;
                    text-align: right;
                    transition: opacity 0 .2s;
                }

                .result {
                    transform-origin: 50% 0;
                }

                .label {
                    opacity: 0;
                    transform-origin: 100% 100%;
                    white-space: nowrap;
                }

                .text {
                    height: 100%;
                    transform-origin: 100% 100%;
                }
            }

            > .buttons {
                height: 72.5%;
                transform-origin: 50% 0;
                transition: transform .4s;

                > .row {
                    display: flex;
                    height: 20%;
                    width: 100%;

                    &:not(:last-of-type) {
                        border-bottom: 1px solid $grey-700;
                    }
                }
            }
        }

        > .controls {
            display: flex;
            left: 0;
            position: absolute;
            top: 8px;
            z-index: 1;

            &:hover > span {
                &:before,
                &:after {
                    opacity: 1;
                }
            }

            > span {
                $size: 12px;
                $icon-height: 2px;
                $icon-width: 8px;
                border-radius: 50%;
                display: block;
                height: $size;
                margin-left: 8px;
                position: relative;
                width: $size;

                &:before, &:after {
                    background-color: $black-500;
                    content: '';
                    display: block;
                    height: $icon-height;
                    left: calc(50% - #{$icon-width / 2});
                    opacity: 0;
                    position: absolute;
                    top: calc(50% - #{$icon-height / 2});
                    width: $icon-width;
                }

                &.amber {
                    background-color: $amber-500;
                }

                &.green {
                    background-color: $green-500;
                    &:before {
                        transform: rotateZ(90deg);
                    }
                }

                &.red {
                    background-color: $red-500;
                    &:before {
                        transform: rotateZ(45deg);
                    }
                    &:after {
                        transform: rotateZ(-45deg);
                    }
                }
            }
        }
    }

    .key {
        background-color: $grey-300;
        cursor: pointer;
        display: flex;
        flex-direction: column;
        justify-content: center;
        position: relative;
        text-align: center;
        transform: translate3d(0);
        user-select: none;
        width: 25%;

        &:not(:first-of-type) {
            border-left: 1px solid $grey-700;
        }

        &:hover {
            &.orange {
                color: $grey-500;
            }
            &:before {
                background-color: rgba(0, 0, 0, 0.1);
                content: '';
                display: block;
                height: 100%;
                left: 0;
                position: absolute;
                top: 0;
                width: 100%;
            }
        }

        &:active {
            &.orange {
                color: $grey-700;
            }
            &:before {
                background-color: rgba(0, 0, 0, 0.2);
                content: '';
                display: block;
                height: 100%;
                left: 0;
                position: absolute;
                top: 0;
                width: 100%;
            }
        }

        &.orange {
            background-color: $orange-500;
            color: #fff;
        }

        &.grey {
            background-color: $grey-500;
        }

        &.wide {
            width: 50%;
        }

        &.no-border-bottom {
            border-bottom: 0;
        }

        .minus {
            position: relative;
            top: -4px;
        }
    }
</style>
