<template>
  <div :style="{height:height}" style="width: '100%'"></div>
</template>

<script>
export default {
  name: "charts",
  props: {
    height: {
      type: String,
      default: () => {
        return "300px"
      }
    },
    title: {
      type: String,
      default: ''
    },
    data: {
      type: Array,
      default: () => []
    },
  },
  data() {
    return {
      chart: null
    };
  },
  mounted() {
    if(this.data && this.data.length){
       this.initChart();
    }
  },
  watch: {
    data: {
      deep: true,
      handler (val) {
        this.initChart(val)
      }
    }
  },
  beforeDestroy() {
    if (!this.chart) {
      return;
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    setOptions() {
      this.chart.setOption({
        title: {
          show: !!this.title,
          text: this.title,
          x: 'center',
          y: 'top',
        },
        tooltip: {
          confine: true,
        },
        calculable: true,
        grid: {
          containLabel: true 
        },
        xAxis: {
          data: this.data.map(item => item.name)
        },
        yAxis: {},
        series: [
          {
            name: "",
            type: "bar",
            barWidth: 20,
            data: this.data.map(item => item.value)
          }
        ]
      }, true);
    },
    initChart() {
      this.chart = this.$echarts.init(this.$el);
      this.setOptions();
      
      window.addEventListener('resize', () => {
        if (!this.chart) return
        this.chart.resize()
      })
    }
  }
};
</script>
