<template>
    <header class="header" :class="theme">
        <div class="header__container">
            <h2 class="header__title">{{title}}</h2>

            <button class="header__filter-btn" @click="emitToggleFilter">
                Filter
                <span class="header__filter-btn-icons">
                    <Funnel v-if="!filterVisible" />
                    <Close v-else />
                </span>
            </button>

            <div class="header__toggle" @click="emitToggleTheme">
                <div class="header__toggle-knob">
                    <Sun />
                    <Moon />
                </div>
            </div>
        </div>

    </header>
</template>

<script>
    import Funnel from './icons/Funnel.vue'
    import Close from './icons/Close.vue'
    import Sun from './icons/Sun.vue'
    import Moon from './icons/Moon.vue'

    export default {
        components: {Funnel, Close, Sun, Moon},
        props: ['theme', 'title', 'filterVisible'],
        methods: {
            emitToggleFilter() {
                this.$emit('toggleFilter')
            },
            emitToggleTheme() {
                this.$emit('toggleTheme')
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
        height: 50px;
        padding: 5px 0;
        z-index: 3;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: background-color $tr-default;
        &.light {
            background-color: $c-white;
        }
        &.dark {
            background-color: $c-cod-grey;
        }
        &__container {
            display: flex;
            align-items: center;
            justify-content: flex-end;
            gap: 0 $gtr-hlf;
            @media (min-width: 576px) {
                gap: 0 $gtr;
            }
        }
        &__title {
            margin: 0 auto 0 0;
        }
        &__filter-btn-icons {
            width: $icon-size;
            height: $icon-size;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            .icon {
                position: absolute;
                top: 0;
                right: 0;
                bottom: 0;
                left: 0;
                margin: auto;
            }
        }
        &__toggle {
            position: relative;
            width: 88px;
            height: 36px;
            overflow: hidden;
            border-radius: 18px;
            cursor: pointer;
            border: 2px solid transparent;
            transition: border-color $tr-default, opacity $tr-default;
            &:hover {
                opacity: .6;
            }
            .light & {
                border-color: $c-dodger-blue;
            }
            .dark & {
                border-color: $c-ocean-green;
            }
            &-knob {
                position: relative;
                left: 5px;
                top: 5px;
                width: 23px;
                height: 23px;
                border-radius: 50%;
                transition: transform $tr-icon, background-color $tr-icon;
                .light & {
                    background-color: $c-dodger-blue;
                    .icon.--sun {
                        transition-delay: $tr-duration-hlf;
                    }
                    .icon.--moon {
                        opacity: 0;
                    }
                }
                .dark & {
                    background-color: $c-ocean-green;
                    transform: translateX(34px);
                    .icon.--sun {
                        opacity: 0;
                    }
                    .icon.--moon {
                        transition-delay: $tr-duration;
                    }
                    @media (min-width: 576px) {
                        transform: translateX(50px);
                    }
                }
                .icon {
                    position: absolute;
                    top: 0;
                    right: 0;
                    bottom: 0;
                    left: 0;
                    margin: auto;
                    transition: opacity $tr-default;
                    &.--sun {
                        fill: $c-white;
                    }
                    &.--moon {
                        fill: $c-cod-grey;
                    }
                }
            }
        }
    }
</style>