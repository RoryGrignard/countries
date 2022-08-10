<template>
    <div class="modal" :class="theme" @click.self="emitHideModal">
        <div class="modal__container" v-for="activeCountry in country" :key="activeCountry.ccn3">
            <div class="modal__head">
                <div class="modal__img-wrapper">
                    <img class="modal__img" :src="activeCountry.flags.svg" :alt="activeCountry.name.common + ' flag'">
                </div>
                <h1 class="modal__title">{{activeCountry.name.common}}</h1>
                <div class="modal__close-btn" @click="emitHideModal"></div>
            </div>
            <ul class="modal__list">
                <li class="modal__list-item">
                    <span>Capital city: </span>
                    <span>{{activeCountry.capital[0]}}</span>
                </li>
                <li class="modal__list-item">
                    <span>Official currencies: </span>
                    <span>
                        <span v-for="(currency, abreviation, index) in activeCountry.currencies" :key="currency.index">
                            <span v-if="index != 0">, </span>
                            {{currency.name}}
                        </span>
                    </span>
                </li>
                <li class="modal__list-item">
                    <span>Population count: </span>
                    <span>{{activeCountry.population}}</span>
                </li>
                <li class="modal__list-item">
                    <span>Alpha-3 ISO code: </span>
                    <span>{{activeCountry.cca3}}</span>
                </li>
                <li class="modal__list-item">
                    <span>Official languages: </span>
                    <span>
                        <span v-for="(language, abreviation, index) in activeCountry.languages" :key="index">
                            <span v-if="index != 0">, </span>
                            {{language}}
                        </span>
                    </span>
                </li>
            </ul>
            
        </div>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity'
    export default {
        props: ['theme', 'country'],
        methods: {
            emitHideModal() {
                this.$emit('hideModal')
            }
        }
    }
</script>

<style lang="scss">
.modal {
    position: fixed;
    top: 0;
    right: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    backdrop-filter: blur(10px);
    z-index: 1;
    transition: background-color $tr-default;
    &.light {
        background-color: $c-white-tr-8;
    }
    &.dark {
        background-color: $c-cod-grey-tr-8;
    }
    &__container {
        width: calc(100% - 40px);
        max-width: 691px;
        padding: $gtr-dbl;
        z-index: 1;
        box-shadow: $box-shadow;
        transition: background-color $tr-default;
        .light & {
            background-color: $c-white;
        }
        .dark & {
            background-color: $c-cod-grey;
        }
    }
    &__head {
        display: flex;
        align-items: center;
        gap: 0 $gtr-dbl;
        position: relative;
        margin: 0 0 $gtr-dbl;
    }
    &__close-btn {
        width: 20px;
        height: 20px;
        position: absolute;
        top: 0;
        right: 0;
        &:before,
        &:after {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            margin: auto;
            width: 20   px;
            height: 2px;
            transition: background-color $tr-default;
            .modal__close-btn:hover & {
                cursor: pointer;
            }
            .light & {
                background-color: $c-cod-grey;
            }
            .dark & {
                background-color: $c-white;
            }
        }
        &:before {
            transform: rotate(-45deg);
        }
        &:after {
            transform: rotate(45deg);
        }
        &:hover {
            cursor: pointer;
            &:before,
            &:after {
                .light & {
                    background-color: $c-dodger-blue-tr-6;
                }
                .dark & {
                    background-color: $c-ocean-green-tr-6;
                }
            }
        }
    }
    &__title {
        margin: 0;
    }
    &__img-wrapper {
        position: relative;
        width: 150px;
        height: 84px;
    }
    &__img {
        position: absolute;
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
    &__list {
        padding: 0;
        display: flex;
        flex-wrap: wrap;
        gap: 20px 0;
        &-item {
            width: 100%;
            list-style: none;
            display: flex;
            gap: 0 $gtr;
            span {
                width: 50%;
            }
        }
    }
}
</style>