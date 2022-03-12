<template>
    <h2>{{ text }}</h2>
    <div>{{ timeStamp }}</div>
</template>

<script>
import moment from 'moment'

export default {
    name: 'DataTitle',
    props: ['text', 'dataDate'],
    computed: {
        timeStamp: function () {
            return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
        },
    },
}
</script>

<style></style>
