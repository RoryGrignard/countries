<template>
    <main class="grid" :class="theme">
        <div class="grid__container">
            <TransitionGroup name="fade">
                <div class="grid__item" v-for="country of countries" :key="country.ccn3" @click="emitShowModal(country.ccn3)">
                    <div class="grid__item-img-wrapper">
                        <img class="grid__item-img" :src="country.flags.svg" :alt="country.name.common + ' flag'">
                    </div>
                    <h3 class="grid__item-title">{{country.name.common}}</h3>
                </div>
            </TransitionGroup>
        </div>
    </main>
</template>

<script>
    export default {
        props: ['theme', 'countries'],
        methods: {
            emitShowModal(countryCCN3) {
                this.$emit('showModal', countryCCN3)
            }
        }
    }
</script>

<style lang="scss">

.grid {
    flex: 1 0 auto;
    padding: $header-height 0;
    transition: background-color $tr-default;
    &.light {
        background-color: $c-white;
    }
    &.dark {
        background-color: $c-cod-grey;
    }
    &__container {
        display: flex;
        flex-wrap: wrap;
        gap: $gtr-dbl $gtr;
    }
    &__item {
        width: calc((100% - 20px) / 2);
        transition: opacity $tr-default;
        &:hover {
            cursor: pointer;
            opacity: 0.7;
        }
        @media (min-width: 768px) {
            width: calc((100% - 60px) / 4);
        }
        @media (min-width: 992px) {
            width: calc((100% - 100px) / 6);
        }
        &-img-wrapper {
            width: 100%;
            position: relative;
            padding: $rat-16-9;
            margin: 0 0 $gtr-hlf;
        }
        &-img {
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            margin: auto;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        &-title {
            margin: 0   ;
        }
    }
}
</style>