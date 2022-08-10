<template>
    <div class="filter" :class="theme">
        <form class="filter__container">
                <div class="filter__wrapper">
                    <label class="filter__label" for="search">Search</label>
                    <input class="filter__input" id="search" type="text" v-model="searchQuery" @keyup="emitSearchQuery(searchQuery)">
                </div>
                <div class="filter__wrapper">
                    <label class="filter__label" for="region">Region</label>
                    <select aria-placeholder="Region" id="region" class="filter__select" v-model="selectedRegion" @change="emitFilterRegion(selectedRegion)">
                        <option value="" disabled>Select region</option>
                        <option value="africa">Africa</option>
                        <option value="americas">Americas</option>
                        <option value="asia">Asia</option>
                        <option value="europe">Europe</option>
                        <option value="oceania">Oceania</option>
                    </select>
                </div>
                <div class="filter__wrapper">
                    <button class="filter__reset-btn" type="button" @click="emitResetFilters">Reset</button>
                </div>
        </form>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                searchQuery: null,
                selectedRegion: null,
            }
        },
        props: ['theme'],
        methods: {
            emitFilterRegion(selectedRegion) {
                this.searchQuery = null
                this.$emit('filterRegion', selectedRegion)
            },
            emitSearchQuery(searchQuery) {
                this.selectedRegion = null
                this.searchQuery = searchQuery
                this.$emit('searchQuery', searchQuery)
            },
            emitResetFilters() {
                this.searchQuery = null
                this.selectedRegion = null
                this.$emit('resetFilters')
            }
        }
    }
</script>

<style lang="scss">
.filter {
    position: fixed;
    top: 0;
    right: 0;
    width: 100%;
    box-shadow: $box-shadow-light;
    z-index: 2;
    padding: $gtr-hlf 0;
    margin: 50px 0 0;
    transition: background-color $tr-default, box-shadow $tr-default;
    @media (min-width: 768px) {
        padding: 7px 0;
    }
    &.light {
        background-color: $c-dodger-blue;
        box-shadow: $box-shadow-light;
    }
    &.dark {
        background-color: $c-ocean-green;
        box-shadow: $box-shadow-dark;
    }
    &__container {
        display: flex;
        flex-wrap: wrap;
        gap: $gtr-hlf;
        @media (min-width: 768px) {
            flex-wrap: nowrap;
            gap: 0 $gtr;
        }
    }
    &__wrapper {
        display: flex;
        align-items: baseline;
        gap: 0 20px;
        width: 100%;
        @media (min-width: 768px) {
            width: calc(100% / 3);
        }
    }
    &__label {
        font-family: 'Roboto Slab', serif;
        transition: color $tr-default, border-color $tr-default;
        &:hover {
            cursor: pointer;
            color: $c-white;
            border-color: $c-white;
        }
       .dark & {
            color: $c-pickled-bluewood;
            border-color: $c-pickled-bluewood;
            &:hover {
            color: $c-white;
            border-color: $c-white;
        }
        }
    }
    &__input,
    &__select {
        border: none;
        width: 100%;
        padding: $gtr-hlf $gtr;
        @media (min-width: 768px) {
            max-width: 200px;
        }
    }
    &__reset-btn {
        margin:  0 0 0 auto;
        .light & {
            color: $c-cod-grey;
            border-color: $c-cod-grey;
            &:hover,
            &:focus {
                color: $c-white;
                border-color: $c-white;
            }
        }
        .dark & {
            color: $c-pickled-bluewood;
            border-color: $c-pickled-bluewood;
            &:hover,
            &:focus {
                color: $c-white;
                border-color: $c-white;
            }
        }
    }
}
</style>