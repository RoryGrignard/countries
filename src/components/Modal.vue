<template>
    <div class="modal" :class="theme">
        <div class="modal__container">
            <h3>Hello World</h3>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['theme']
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
    backdrop-filter: blur(5px);
    z-index: 2;
    visibility: hidden;
    transition: background-color $trans-default;
    &.visible {
        visibility: visible;
    }
    &.light {
        background-color: $c-white-semi-trans;
    }
    &.dark {
        background-color: $c-cod-grey-semi-trans;
    }
    &__container {
        width: calc(100% - 40px);
        max-width: 600px;
        padding: $gtr;
        z-index: 1;
        box-shadow: $box-shadow;
        transition: background-color $trans-default;
        .light & {
            background-color: $c-white;
        }
        .dark & {
            background-color: $c-cod-grey;
        }
    }
}
</style>