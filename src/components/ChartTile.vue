<template>
    <tile :position="position" :heading="heading" :color="color">
        <bar-chart class="chart" :data="data" :options="options" v-if="type == 'bar'"></bar-chart>
        <line-chart class="chart" :data="data" :options="options" v-if="type == 'line'"></line-chart>
        <update-prop-chart class="chart" :data="data" :options="options"  :chart-data="localData" v-if="type == 'update-prop'"></update-prop-chart>
        <doughnut-chart class="chart" :data="data" :options="options" v-if="type == 'doughnut'"></doughnut-chart>
    </tile>
</template>

<script>
import Tile from './atoms/Tile';
import BarChart from './charts/BarChart'
import LineChart from './charts/LineChart'
import UpdatePropChart from './charts/UpdatePropChart'
import DoughnutChart from './charts/DoughnutChart'

export default {

    extends: Tile,

    components: {
        Tile,
        BarChart,
        LineChart,
        UpdatePropChart,
        DoughnutChart
    },

    props: ['data', 'options', 'type'],

    data: function() {
        return {
            localData: {}
        };
    },

    watch: {
        data: function() {
            this.localData = this.data;
        }
    }
}
</script>

<style lang="scss">

    @import "../assets/styles/_vars.scss";

    .chart {
        flex: 1 0 100%;
        align-self: stretch;
        width: 100%;
    }

</style>
