<template>
    <header class="header" :class="theme">
        <div class="header__container">
            <h1 class="header__title">{{title}}</h1>

            <div class="header__toggle" @click="changeTheme">
                <div class="header__toggle-knob"></div>
                <div class="header__toggle-layer"></div>
            </div>
        </div>

    </header>
</template>

<script>
    export default {
        props: ['theme', 'title'],
        methods: {
            changeTheme() {
                this.$emit('change')
            }
        }
    }
</script>


<style lang="scss">
.header {
    position: fixed;
    top: 0;
    right: 0;
    width: 100%;
    padding: 5px 0;
    box-shadow: $box-shadow;
    z-index: 1;
    transition: background-color $trans-default;
    &.light {
        background-color: $c-white-semi-trans;
    }
    &.dark {
        background-color: $c-cod-grey-semi-trans;
    }
    &__container {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    &__title {
        margin: 0;
    }
    &__toggle {
        position: relative;
        width: 74px;
        height: 36px;
        overflow: hidden;
        border-radius: 100px;
        cursor: pointer;
        &-knob,
        &-layer {
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            transition: 0.3s ease all;
        }
        &-layer {
            width: 100%;
            transition: 0.3s ease background-color;
            z-index: 1;
            border-radius: 100px;
            transition: background-color $trans-default;
            .light & {
                background-color: $c-dodger-blue-semi-trans;
            }
            .dark & {
                background-color: $c-ocean-green-semi-trans;
            }
        }
        &-knob {
            position: relative;
            width: 100%;
            height: 100%;
            z-index: 2;
            &:before {
                position: absolute;
                top: 4px;
                left: 6px;
                width: 28px;
                height: 28px;
                border-radius: 50%;
                transition: transform $trans-default, background-color $trans-default;
                .light & {
                    content: '';
                    background-color: $c-dodger-blue;
                }
                .dark & {
                  content: '';
                  transform: translateX(34px);
                  background-color: $c-ocean-green;
                }
            }
        }
    }
}

</style>