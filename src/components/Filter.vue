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
            }
        }
    }
</script>

<style lang="scss">
    .filter {
        padding: $gtr-hlf 0;
        margin: 50px 0 0;
        transition: background-color $tr-default;
        @media (min-width: 768px) {
            padding: 7px 0;
        }
        &.light {
            background-color: $c-dodger-blue;
        }
        &.dark {
            background-color: $c-ocean-green;
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
                width: 50%;
            }
        }
        &__label {
            font-family: 'Roboto Slab', serif;
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
    }
</style>