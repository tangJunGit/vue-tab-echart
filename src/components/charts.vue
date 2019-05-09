<template>
  <div :style="{height:props.height,width:props.width}"></div>
</template>

<script>
export default {
  name: "charts",
  props: {
    props: {
      type: Object,
      default: {
        width: "100%",
        height: "300px"
      }
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