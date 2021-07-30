<script>
import { defineComponent } from "vue";
import { Line } from "vue3-chart-v2";
// const { reactiveProp } = mixins;

export default defineComponent({
  name: "MonthlyChart",
  extends: Line,
  // mixins: [Line.mixins.reactiveProp],
  props: {
    chartData: {
      type: Object,
      required: true,
    },
    // chartOptions: {
    //   type: Object,
    //   required: false,
    // },
  },
  data() {
    return {
      myOptions: {
        scaleOverride: true,
        scaleSteps: 1,
        scaleStepWidth: 50,
        scaleStartValue: 0,
      },
    };
  },
  watch: {
    chartData() {
      this.renderChart(this.chartData, {
        scales: {
          yAxes: [
            {
              ticks: {
                min: 0,
                max: 50,
                stepSize: 10,
                reverse: false,
                beginAtZero: true,
              },
            },
          ],
        },
      });
      // console.log(this.myOptions);
    },
  },
  mounted() {
    // console.log(this.myOptions);
    this.renderChart(this.chartData, {
      scales: {
        yAxes: [
          {
            ticks: {
              min: 0,
              max: 50,
              stepSize: 10,
              reverse: false,
              beginAtZero: true,
            },
          },
        ],
      },
    });
    // this.height=300
  },
});
</script>

<style>
canvas {
  max-height: 450px !important;
}
</style>