<script>
import { Line, mixins } from 'vue-chartjs'

const { reactiveData } = mixins

export default {

  extends: Line,

  mixins: [reactiveData],

  data: function data() {
    return {
      data: [],
      labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
      chartData: '',
      options: {
        responsive: true,
        maintainAspectRatio: false
      }
    };
  },

  created: function created() {
    this.fillData();
  },

  mounted: function mounted() {
    var self = this;

    this.renderChart(this.chartData, this.options);
    setInterval(function () {
        self.fillData();
    }, 2000);
  },

  methods: {

    fillData: function fillData() {
      this.addData();
      this.chartData = {
        labels: this.labels,
        datasets: [{
          label: 'Live Data',
          backgroundColor: '#e67e22',
          data: this.data
        }]
      };
    },

    addData: function () {
        this.data.push(this.getRandomInt());
        if(this.data.length > this.labels.length) {
            this.data.shift();
            this.labels.push(this.labels.shift());
        }
    },

    getRandomInt: function getRandomInt() {
      return Math.floor(Math.random() * (50 - 5 + 1)) + 5;
    }

  }
};
</script>