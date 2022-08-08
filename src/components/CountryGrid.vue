<template>
    <main class="country-grid" :class="theme">
        <div class="country-grid__container">
            <div class="country-grid__item">
                <h3>Hello World</h3>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vitae, modi in sapiente dolores aut sed incidunt necessitatibus? Animi recusandae, necessitatibus non qui minima itaque dignissimos voluptatem iure, atque culpa nobis.</p>
            </div>
        </div>
    </main>
</template>

<script>
    export default {
        props: ['theme']
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
        gap: $gtr;
    }
    &__item {
        width: calc((100% - 20px) / 2);
        @media (min-width: 767px) {
            width: calc((100% - 60px) / 4);
        }
        @media (min-width: 992px) {
            width: calc((100% - 100px) / 6);
        }
    }
}
</style>