<template>
    <main class="country-grid" :class="theme">
        <div class="country-grid__container">
            <div class="country-grid__item" v-for="country of countries" :key="country.id">
                <div class="country-grid__item-img-wrapper">
                    <img :src="country.flags.svg" :alt="country.name.common" class="country-grid__item-img">
                </div>
                <h3 class="country-grid__item-title">{{country.name.common}}</h3>
            </div>
        </div>
    </main>
</template>

<script>
    export default {
        props: ['theme', 'countries']
    }
</script>

<style lang="scss">
.country-grid {
    flex: 1 0 auto;
    padding: $header-height-bdl 0;
    transition: background-color $trans-default;
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
        @media (min-width: 767px) {
            width: calc((100% - 60px) / 4);
        }
        @media (min-width: 992px) {
            width: calc((100% - 100px) / 6);
        }
        &-img-wrapper {
            width: 100%;
            position: relative;
            padding: $ratio-16-x-9;
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