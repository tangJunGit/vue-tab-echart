<template>
  <div :style="{height:height,width:width}"></div>
</template>

<script>
export default {
  name: "charts",
  props: {
    width: {
      type: String,
      default: "100%"
    },
    height: {
      type: String,
      default: "300px"
    },
    data: {
      type: Object,
      default: null
    },
  },
  data: function() {
    return {
      chart: null
    };
  },
  mounted: function() {
    if(this.data !== null){
       this.initChart();
    }
  },
  beforeDestroy: function() {
    if (!this.chart) {
      return;
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    setOptions: function() {
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
    initChart: function() {
      this.chart = this.$echarts.init(this.$el);
      this.setOptions();
    }
  }
};
</script>

<style scoped>
</style>