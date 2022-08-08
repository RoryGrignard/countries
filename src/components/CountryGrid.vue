<template>
    <main class="country-grid" :class="theme">
        <div class="country-grid__container">
            <div class="country-grid__item">
                
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
    &.dark {
        background-color: rgb(0, 0, 0);
    }
    &.light {
        background-color: rgb(255, 255, 255);
    }
}
</style>