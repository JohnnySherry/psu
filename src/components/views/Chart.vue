<template>
<div>
    <div>
       <button v-on:click="getdata">click</button>
       <vue-chart type="line" :data="mydata" :options="myoptions"></vue-chart>
       <vue-chart type="bar" v-for="item in items" v-bind:data="item" v-bind:key="item.index" v-bind:options="myoptions"></vue-chart>
   </div> 
    <div class="row">
      <div class="box">
        <div class="box-header with-border">
          <h3 class="box-title"></h3>
          <div class="box-body">
            <hr class="visible-xs-block">
            <div>
              <p class="text-center">
                <strong>Powersupply issues Overview</strong>
              </p>
              <canvas id="languagePie"></canvas>
            </div>
          </div>
        </div>
        <div class="text-center">
          <small><b>Pro Tip</b> Don't forget to star us on github!</small>
        </div>
      </div>
   </div>
</div>
   
    
</template>

<script>
import VueChart from 'vue-chart'
import api from '../../api'

export default {
    data () {
        return {
            items:[
                {
                     labels: ["January", "February", "March", "April", "May", "June", "July"],
                     datasets: [
                        {
                        label: "My First dataset",
                        fillColor: "rgba(220,220,220,0.5)",
                        strokeColor: "rgba(220,220,220,0.8)",
                        highlightFill: "rgba(220,220,220,0.75)",
                        highlightStroke: "rgba(220,220,220,1)",
                        data: [65, 59, 80, 81, 56, 55, 40]
                        },
                    ]
                },
                {
                     labels: ["January", "February", "March", "April", "May", "June", "July"],
                     datasets: [
                        {
                        label: "My second dataset",
                        fillColor: "rgba(220,220,220,0.5)",
                        strokeColor: "rgba(220,220,220,0.8)",
                        highlightFill: "rgba(220,220,220,0.75)",
                        highlightStroke: "rgba(220,220,220,1)",
                        data: [35, 26, 11, 81, 67, 90, 40]
                        },
                    ]
                }
            ],
            datakey :[],
            dataValue :[],
            mydata:{
            labels: ["January", "February", "March", "April", "May", "June", "July"],
            datasets: [
            {
            label: "My First dataset",
            fillColor: "rgba(220,220,220,0.2)",
            strokeColor: "rgba(220,220,220,1)",
            pointColor: "rgba(220,220,220,1)",
            pointStrokeColor: "#fff",
            pointHighlightFill: "#fff",
            pointHighlightStroke: "rgba(220,220,220,1)",
            data: [65, 59, 80, 81, 56, 55, 40]
            },
            {
            label: "My Second dataset",
            fillColor: "rgba(151,187,205,0.2)",
            strokeColor: "rgba(151,187,205,1)",
            pointColor: "rgba(151,187,205,1)",
            pointStrokeColor: "#fff",
            pointHighlightFill: "#fff",
            pointHighlightStroke: "rgba(151,187,205,1)",
            data: [28, 48, 40, 19, 86, 27, 90]
            }
            ]
            },
            myoptions:{
                 scaleShowGridLines : true,

            //String - Colour of the grid lines
            scaleGridLineColor : "rgba(0,0,0,.05)",

            //Number - Width of the grid lines
            scaleGridLineWidth : 1,

            //Boolean - Whether to show horizontal lines (except X axis)
            scaleShowHorizontalLines: true,

            //Boolean - Whether to show vertical lines (except Y axis)
            scaleShowVerticalLines: true,

            //Boolean - Whether the line is curved between points
            bezierCurve : true,

            //Number - Tension of the bezier curve between points
            bezierCurveTension : 0.4,

            //Boolean - Whether to show a dot for each point
            pointDot : true,

            //Number - Radius of each point dot in pixels
            pointDotRadius : 4,

            //Number - Pixel width of point dot stroke
            pointDotStrokeWidth : 1,

            //Number - amount extra to add to the radius to cater for hit detection outside the drawn point
            pointHitDetectionRadius : 20,

            //Boolean - Whether to show a stroke for datasets
            datasetStroke : true,

            //Number - Pixel width of dataset stroke
            datasetStrokeWidth : 2,

            //Boolean - Whether to fill the dataset with a colour
            datasetFill : true,

            //String - A legend template
            legendTemplate : "<ul class=\"<%=name.toLowerCase()%>-legend\"><% for (var i=0; i<datasets.length; i++){%><li><span style=\"background-color:<%=datasets[i].strokeColor%>\"></span><%if(datasets[i].label){%><%=datasets[i].label%><%}%></li><%}%></ul>"

            }
        }
    },
    components:{
        VueChart
    },
    methods:{
        getData(){
          api.request('get','/api/fv').then(res=>{
            this.datakey=res.data.key
            this.dataValue=res.data.value
          }).then(()=>{
          var barChartCanvas = document.getElementById('languagePie').getContext('2d')
          var barConfig = {
            type: 'bar',
            data: {
              labels: this.datakey,
              datasets: [{
                        label: "Powersupply issue",
                        fillColor: "rgba(220,220,220,0.5)",
                        strokeColor: "rgba(220,220,220,0.8)",
                        highlightFill: "rgba(220,220,220,0.75)",
                        highlightStroke: "rgba(220,220,220,1)",
                        data:this.dataValue
                        }]
            },
            options: {
              responsive: true,
              maintainAspectRatio: !this.isMobile,
              legend: {
                position: 'bottom',
                display: true
              }
            }
          }

          new Chart(barChartCanvas, barConfig) // eslint-disable-line no-new

          })
        } 
    },
    mounted(){
        this.getData()
    }    
}
</script>