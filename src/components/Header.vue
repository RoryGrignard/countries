<template>
    <header class="header" :class="theme">
        <img class="header__logo" alt="Vue logo" src="../assets/logo.png">
        <h1 class="header__title">{{title}}</h1>
    </header>
</template>

<script>
    export default {
        props: ['theme', 'title']
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
}
</style>