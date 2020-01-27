<template>
    <div class="content">
        <div class="row">
            <div class="col-12">
                <card
                        type="chart"
                >
                    <template slot="header">
                        <div class="row">
                            <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                                <template v-if="!isRTL">
                                    <h5 class="card-category">Networking</h5>
                                </template>
                                <template v-else>
                                    <h5 class="card-category">Category</h5>
                                </template>
                                <template v-if="!isRTL">
                                    <h2 class="card-title">Performance</h2>
                                </template>
                            </div>
                            <div class="col-sm-6">
                                <div class="btn-group btn-group-toggle"
                                     data-toggle="buttons"
                                     :class="isRTL ? 'float-left' : 'float-right'">
                                    <template v-if="!isRTL">
                                        <label v-for="(option, index) in bigLineChartCategories"
                                               :key="option"
                                               class="btn btn-success btn-sm btn-simple"
                                               :class="{active:bigLineChart.activeIndex === index}"
                                               :id="index">
                                            <input type="radio"
                                                   @click="initBigChart(index)"
                                                   name="options" autocomplete="off"
                                                   :checked="bigLineChart.activeIndex === index">
                                            {{ option }}
                                        </label>
                                    </template>
                                    <template v-else>
                                        <label v-for="(option, index) in bigLineChartCategoriesAr"
                                               :key="option"
                                               class="btn btn-success btn-sm btn-simple"
                                               :class="{active:bigLineChart.activeIndex === index}"
                                               :id="index">
                                            <input type="radio"
                                                   @click="initBigChart(index)"
                                                   name="options" autocomplete="off"
                                                   :checked="bigLineChart.activeIndex === index">
                                            {{ option }}
                                        </label>
                                    </template>
                                </div>
                            </div>
                        </div>
                    </template>
                    <line-chart
                            class="chart-area"
                            ref="bigChart"
                            chart-id="big-line-chart"
                            :chart-data="bigLineChart.chartData"
                            :gradient-colors="bigLineChart.gradientColors"
                            :gradient-stops="bigLineChart.gradientStops"
                            :extra-options="bigLineChart.extraOptions">
                    </line-chart>
                </card>
            </div>
        </div>
        <div class="row">
            <div class="col-lg-4" :class="{'text-right': isRTL}">
                <card
                        type="chart"
                        cardCol
                >
                    <template slot="header">
                        <h5 class="card-category">Cisco IOS Tasks</h5>
                        <!--<h5 class="card-category">{{$t('dashboard.totalShipments')}}</h5>-->
                        <h3 class="card-title"><i class="tim-icons icon-bell-55 text-primary "></i> 763,215</h3>
                    </template>
                    <line-chart
                            class="chart-area"
                            chart-id="green-line-chart"
                            :chart-data="greenLineChart.chartData"
                            :gradient-colors="greenLineChart.gradientColors"
                            :gradient-stops="greenLineChart.gradientStops"
                            :extra-options="greenLineChart.extraOptions">
                    </line-chart>
                </card>
            </div>
            <div class="col-lg-4">
                <card
                        type="chart"
                        cardCol
                >
                    <template slot="header">
                        <h5 class="card-category">IoT sensors</h5>
                        <!--<h5 class="card-category">{{$t('dashboard.dailySales')}}</h5>-->
                        <h3 class="card-title"><i class="tim-icons icon-alert-circle-exc text-info "></i> 3,500</h3>
                    </template>
                    <bar-chart
                            class="chart-area"
                            chart-id="blue-bar-chart"
                            :chart-data="blueBarChart.chartData"
                            :gradient-stops="blueBarChart.gradientStops"
                            :extra-options="blueBarChart.extraOptions">
                    </bar-chart>
                </card>
            </div>
            <div class="col-lg-4">
                <card
                        type="chart"
                        cardCol
                >
                    <template slot="header">
                        <h5 class="card-category">Webex messages</h5>
                        <!--//<h5 class="card-category">{{$t('dashboard.completedTasks')}}</h5>-->
                        <h3 class="card-title"><i class="tim-icons icon-send text-success "></i> 12,100K</h3>
                    </template>
                    <line-chart
                            class="chart-area"
                            chart-id="purple-line-chart"
                            :chart-data="purpleLineChart.chartData"
                            :gradient-stops="purpleLineChart.gradientStops"
                            :extra-options="purpleLineChart.extraOptions">
                    </line-chart>
                </card>
            </div>
        </div>
        <div class="row">
            <div class="col-lg-6 col-md-12">
                <card type="tasks">
                    <template slot="header">
                        <template v-if="!isRTL">
                            <h6 class="title d-inline">Tasks(5)</h6>
                        </template>
                        <template v-if="!isRTL">
                            <p class="card-category d-inline">Today</p>
                        </template>
                        <drop-down tag="div" :class="isRTL ? 'float-left' : ''">
                            <button aria-label="Settings menu" data-toggle="dropdown"
                                    class="dropdown-toggle btn-rotate btn btn-link btn-icon"
                                    :class="isRTL ? 'pl-5' : ''">
                                <i class="tim-icons icon-settings-gear-63"></i>
                            </button>
                            <ul class="dropdown-menu dropdown-menu-right">
                                <a href="#pablo" class="dropdown-item">Action</a>
                                <a href="#pablo" class="dropdown-item">Another Action</a>
                                <a href="#pablo" class="dropdown-item">Something else</a>
                            </ul>
                        </drop-down>
                    </template>
                    <div class="table-full-width table-responsive">
                        <task-list></task-list>
                    </div>
                </card>
            </div>
            <div class="col-lg-6 col-md-12">
                <card class="card">
                    <h4 slot="header" class="card-title">
                        <template v-if="!isRTL">
                            Simple Table
                        </template>
                    </h4>
                    <div class="table-responsive">
                        <user-table></user-table>
                    </div>
                </card>
            </div>
        </div>
    </div>
</template>
<script>

    import {
        Card
    } from "@/components/index";

    import LineChart from '@/components/Charts/LineChart';
    import BarChart from '@/components/Charts/BarChart';
    import * as chartConfigs from '@/components/Charts/config';
    import TaskList from './Dashboard/TaskList'
    import UserTable from './Dashboard/UserTable'
    import config from '@/config';
    //import jsxapi from 'jsxapi';
    import axios from 'axios';
    const jsxapi = require('jsxapi');

    //let durationData = [1,2];
    export default {
        components: {
            Card,
            //LineChart,
            BarChart,
            TaskList,
            UserTable
        },
        data() {
            let durationData = [1,2];
            return {
                bigLineChartCategories: [
                    "SLA",
                    "Tickets",
                    "Sessions"
                ],
                bigLineChart: {
                    allData: [
                        [100, 70, 90, 70, 85, 60, 75, 60, 90, 80, 110, 100],
                        [80, 120, 105, 110, 95, 105, 90, 100, 80, 95, 70, 120],
                        [60, 80, 65, 130, 80, 105, 90, 130, 70, 115, 60, 130]
                    ],
                    activeIndex: 0,
                    chartData: {datasets: [{}]},
                    extraOptions: chartConfigs.purpleChartOptions,
                    gradientColors: config.colors.primaryGradient,
                    gradientStops: [1, 0.4, 0],
                    categories: [],
                },
                greenLineChart: {
                    extraOptions: chartConfigs.greenChartOptions,
                    chartData: {
                        labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'],
                        datasets: [{
                            label: "Data",
                            fill: true,
                            borderColor: config.colors.primary,
                            borderWidth: 2,
                            borderDash: [],
                            borderDashOffset: 0.0,
                            pointBackgroundColor: config.colors.primary,
                            pointBorderColor: 'rgba(255,255,255,0)',
                            pointHoverBackgroundColor: config.colors.primary,
                            pointBorderWidth: 20,
                            pointHoverRadius: 4,
                            pointHoverBorderWidth: 15,
                            pointRadius: 4,
                            data: [80, 100, 70, 80, 120, 80],
                        }]
                    },
                    gradientColors: config.colors.primaryGradient,
                    gradientStops: [1, 0.2, 0],
                },
                blueBarChart: {
                    extraOptions: chartConfigs.barChartOptions,
                    chartData: {
                        labels: ['0', '1', '2', '3', '4', '5'],
                        //labels: ['USA1', 'GER', 'AUS', 'UK', 'RO', 'BR'],
                        datasets: [{
                            label: "Countries",
                            fill: true,
                            borderColor: config.colors.info,
                            borderWidth: 2,
                            borderDash: [],
                            borderDashOffset: 0.0,
                            data: [53, 20, 10, 80, 100, 45],
                            //data: this.idData,
                        }]
                    },
                    gradientColors: config.colors.primaryGradient,
                    gradientStops: [1, 0.4, 0],
                },
                purpleLineChart: {
                    extraOptions: chartConfigs.purpleChartOptions,
                    chartData: {
                        labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV'],
                        datasets: [{
                            label: "My First dataset",
                            fill: true,
                            borderColor: config.colors.danger,
                            borderWidth: 2,
                            borderDash: [],
                            borderDashOffset: 0.0,
                            pointBackgroundColor: config.colors.danger,
                            pointBorderColor: 'rgba(255,255,255,0)',
                            pointHoverBackgroundColor: config.colors.danger,
                            pointBorderWidth: 20,
                            pointHoverRadius: 4,
                            pointHoverBorderWidth: 15,
                            pointRadius: 4,
                            data: [90, 27, 60, 12, 80],
                        }]
                    },
                    gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
                    gradientStops: [1, 0.4, 0],
                }
            }
        },
        computed: {
            enableRTL() {
                return this.$route.query.enableRTL;
            },
            isRTL() {
                return this.$rtl.isRTL;
            },

        },
        created() {
            //this.fetchPlaces()

            //console.log('The time is ' . this.$moment().format("HH:mm"));
            this.getRoomKitInfo();
            //   setInterval(() => {
            //     this.getRoomKitInfo()
            //   }, 2000)
        },
        methods: {
            initBigChart(index) {
                let chartData = {
                    datasets: [{
                        fill: true,
                        borderColor: config.colors.primary,
                        borderWidth: 2,
                        borderDash: [],
                        borderDashOffset: 0.0,
                        pointBackgroundColor: config.colors.primary,
                        pointBorderColor: 'rgba(255,255,255,0)',
                        pointHoverBackgroundColor: config.colors.primary,
                        pointBorderWidth: 20,
                        pointHoverRadius: 4,
                        pointHoverBorderWidth: 15,
                        pointRadius: 4,
                        data: this.bigLineChart.allData[index]
                    }],
                    labels: ['JAN', 'FEB', 'MAR', 'APR', 'MAY', 'JUN', 'JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'],
                }
                this.$refs.bigChart.updateGradients(chartData);
                this.bigLineChart.chartData = chartData;
                this.bigLineChart.activeIndex = index;
                console.log(`TEST`);
                console.log("duration blank ", this.durationData);
            },

            // http://172.17.250.91/
            // sandbox let xapi = jsxapi.connect('wss://10.10.20.159', {username: 'admin', password: 'ciscopsdt'});
            getRoomKitInfo() {
                let xapi = jsxapi.connect('wss://172.17.250.91', {username: 'localadmin', password: 'ciscopsdt'});
                // this.idData = [1, 2, 3, 4, 5, 6];
                // xapi.command('Dial', {Number: 'balexey@cisco.com'})
                //     .then((call) => {
                //         console.log(`Started call with status: ${call.status}, id: ${call.CallId}`);
                //
                //         // Stop call after delay
                //         const delay = 30;
                //         console.log(`Call will be disconnected in ${delay} seconds...`);
                //
                //         setTimeout(() => {
                //             console.log('Disconnecting');
                //             xapi.command('Call Disconnect', {CallId: call.CallId})
                //         }, delay * 2000);
                //
                //     })

                xapi.on('ready', ready);

                function ready() {
                    xapi.command("CallHistory Get", {
                        DetailLevel: "Full"
                    })
                        .then((history) => {

                            // Code logic
                            console.log(history);
                            let idData = [];
                            let durationData = [];
                            console.log("Id", history['Entry'][0]['id']);
                            //this.blueBarChart.data = [history['Entry'][0]['id'], history['Entry'][1]['id']];
                            console.log("Length ", history['Entry'].length);
                            for (var i = 0; i < history['Entry'].length; i++) {
                                //console.log("Id-", history['Entry'][i]['id']);
                                idData.push(history['Entry'][i]['id']);
                            }
                            console.log("idData:", idData);

                            for (var i = 0; i < history['Entry'].length; i++) {
                                durationData.push(history['Entry'][i]['Duration']);
                            }
                            console.log("durationData:", durationData);
                            //console.log("DURATION ", history['Entry'][0]['Duration']);

                        });
                }
            },
        },
        mounted() {
            this.i18n = this.$i18n;
            if (this.enableRTL) {
                this.i18n.locale = 'ar';
                this.$rtl.enableRTL();
            }
            this.initBigChart(0);

        },
        beforeDestroy() {
            if (this.$rtl.isRTL) {
                this.i18n.locale = 'en';
                this.$rtl.disableRTL();
            }
        }
    }
</script>
<style>
</style>
