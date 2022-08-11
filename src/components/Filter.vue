<template>
    <div class="filter" :class="[theme, filterVisible ? '--visible' : '', filtered ? '--filtered' : '']">
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
                    <Transition name="fade">
                        <button class="filter__reset-btn" type="button" v-if="filtered" @click="emitResetFilters">
                            Reset
                            <Reset />
                        </button>
                    </Transition>
                </div>
        </form>
    </div>
</template>

<script>
    import Reset from './icons/Reset.vue'

    export default {
        components: {Reset},
        data() {
            return {
                searchQuery: null,
                selectedRegion: null,
            }
        },
        props: ['theme', 'filterVisible', 'filtered'],
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
        z-index: 2;
        padding: $gtr 0 $gtr-hlf;
        margin: 50px 0 0;
        transform: translateY(-118px);
        transition: background-color $tr-default, box-shadow $tr-default, transform     $tr-default;
        &.--filtered {
            transform: translateY(-154px);
        }
        &.--visible {
            transform: translateY(0);
        }
        @media (min-width: 576px) {
            padding: 7px 0;
            transform: translateY(-47px);
            &.--filtered {
                transform: translateY(-47px);
            }
            &.--visible {
                transform: translateY(0);
            }
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
            align-items: center;
            justify-content: space-between;
            gap: $gtr-hlf;
            transition: opacity $tr-default;
            opacity: 0;
            .filter.--visible & {
                opacity: 1;
            }
            @media (min-width: 576px) {
                flex-wrap: nowrap;
                gap: 0 $gtr;
            }
        }
        &__wrapper {
            display: flex;
            align-items: baseline;
            gap: 0 20px;
            width: 100%;
            @media (min-width: 576px) {
                width: calc(100% / 3);
            }
        }
        &__label {
            font-family: 'Roboto Slab', serif;
            align-self: center;
            transition: color $tr-default, border-color $tr-default;
            &:hover {
                cursor: pointer;
                color: $c-white;
                border-color: $c-white;
            }
        }
        &__input,
        &__select {
            border: none;
            width: 100%;
            @media (min-width: 576px) {
                max-width: 200px;
            }
        }
        &__input {
            padding: $gtr-hlf $gtr;
        }
        &__select {
            padding: 9px 20px;
        }
        &__reset-btn {
            margin:  0 0 0 auto;
            .icon {
                transition: fill $tr-default, transform $tr-default;
            }
            .light & {
                color: $c-white;
                border-color: $c-white;
                .icon {
                    fill: $c-white;
                }
            }
            .dark & {
                color: $c-cod-grey;
                border-color: $c-cod-grey;
                .icon {
                    fill: $c-cod-grey;
                }
            }
            &:hover {
                opacity: 1;
                .icon {
                    transform: rotate(360deg);
                }
            }
        }
    }
</style>