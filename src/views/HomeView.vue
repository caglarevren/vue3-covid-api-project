<template>
    <div v-if="!loading">
        <DataTitle :text="title" :dataDate="dataDate" />
        <DataBoxes :stats="stats" />
        <CountrySelect @get-country="getCountryData" :countries="countries" />
        <button @click="clearCountryData" v-if="stats.Country">
            Clear Country
        </button>
    </div>
    <div v-else><img :src="loadingImage" /></div>
</template>

<script>
import DataTitle from '@/components/DataTitle.vue'
import DataBoxes from '@/components/DataBoxes.vue'
import CountrySelect from '@/components/CountrySelect.vue'

export default {
    name: 'HomeView',
    components: { DataTitle, DataBoxes, CountrySelect },
    data() {
        return {
            loading: true,
            title: 'Global',
            dataDate: '',
            status: {},
            countries: [],
            loadingImage: require('../assets/hourglass.gif'),
        }
    },
    methods: {
        async fetchCovidData() {
            const res = await fetch('https://api.covid19api.com/summary')
            const data = await res.json()
            return data
        },
        getCountryData(country) {
            this.stats = country
            this.title = country.Country
        },
        async clearCountryData() {
            this.loading = true
            const data = await this.fetchCovidData()
            this.title = 'Global'
            this.stats = data.Global
            this.loading = false
        },
    },
    async created() {
        const data = await this.fetchCovidData()
        this.dataDate = data.dataDate
        this.stats = data.Global
        this.countries = data.Countries
        this.loading = false
    },
}
</script>
