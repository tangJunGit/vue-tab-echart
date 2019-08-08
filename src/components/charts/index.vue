<template>
  <div :style="{height:props.height,width:props.width}"></div>
</template>

<script>
export default {
  name: "charts",
  props: {
    props: {
      type: Object,
      default: () => {
        return {
          width: "100%",
          height: "300px"
        }
      }
    },
    data: {
      type: Object,
      default: () => null
    },
  },
  data() {
    return {
      chart: null
    };
  },
  mounted() {
    if(this.data !== null){
       this.initChart();
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
        title: { text: this.data.title },
        tooltip: {},
        xAxis: {
          data: this.data.xAxis
        },
        yAxis: {},
        series: [
          {
            name: "",
            type: "bar",
            data: this.data.series
          }
        ]
      });
    },
    initChart() {
      this.chart = this.$echarts.init(this.$el);
      this.setOptions();
      
      window.addEventListener('resize', () => {
        this.chart.resize()
      })
    }
  }
};
</script>
