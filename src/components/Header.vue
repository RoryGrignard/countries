<template>
    <header class="header" :class="theme">
        <img class="header__logo" alt="Vue logo" src="../assets/logo.png">
        <h1 class="header__title">{{title}}</h1>

        <div class="header__toggle" @click="changeTheme">
          <div class="header__toggle-knob"></div>
          <div class="header__toggle-layer"></div>
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
    padding: 5px 20px;
    box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, 0.1);
    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: space-between;
    &.dark {
        background-color: rgba(0, 0, 0, 0.6);
    }
    &.light {
        background-color: rgba(255, 255, 255, 0.6);
    }
    &__logo {
        width: 60px;
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
            .dark & {
                background-color: #ebf7fc;
            }
            .light & {
                background-color: #fcebeb;
            }
        }
        &-knob {
            position: relative;
            width: 100%;
            height: 100%;
            z-index: 2;
            &:before {
                content: "Dark";
                position: absolute;
                top: 4px;
                left: 4px;
                width: 20px;
                height: 10px;
                color: #fff;
                font-size: 10px;
                font-weight: bold;
                text-align: center;
                line-height: 1;
                padding: 9px 4px;
                background-color: #03a9f4;
                border-radius: 50%;
                transition: 0.3s ease background-color, 0.3s ease left;
                .light & {
                  content: "Light";
                  left: 42px;
                  background-color: #f44336;
                }
            }
        }
    }
}

</style>