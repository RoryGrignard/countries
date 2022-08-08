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
    &.visible {
        visibility: visible;
    }
    &.dark {
        background-color: rgba(0, 0, 0, 0.6);
    }
    &.light {
        background-color: rgba(255, 255, 255, 0.6);
    }
    &__container {
        width: calc(100% - 40px);
        max-width: 600px;
        padding: 20px;
        z-index: 1;
        box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, 0.1);
        .modal.dark & {
            background-color: rgb(0, 0, 0);
        }
        .modal.light & {
            background-color: rgb(255, 255, 255);
        }
    }
}
</style>