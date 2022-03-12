<template>
    <h3>Cases</h3>
    <div>
        <p>New: {{ stats.NewConfirmed }}</p>
        <p>Total: {{ stats.TotalConfirmed }}</p>
    </div>
    <h3>Deaths</h3>
    <div>
        <p>New: {{ numberWithCommas(stats.NewDeaths) }}</p>
        <p>Total: {{ numberWithCommas(stats.TotalDeaths) }}</p>
    </div>
</template>

<script>
export default {
    name: 'DataBoxes',
    props: ['stats'],
    methods: {
        numberWithCommas(x) {
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
        },
    },
}
</script>

<style></style>
