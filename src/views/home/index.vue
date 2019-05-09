<template>
  <div>
    <el-tabs type="card" v-model="tabItem">
      <el-tab-pane label="tab1" name="tab1">
        <h1>tab1</h1>
        <charts v-if="'tab1' === tabItem" :props="props" :data="data">tab1</charts>
      </el-tab-pane>
      <el-tab-pane label="tab2" name="tab2">
        <h1>tab2</h1>
        <charts v-if="'tab2' === tabItem" :props="props" :data="data">tab2</charts>
      </el-tab-pane>
      <el-tab-pane label="tab3" name="tab3">
        <h1>tab3</h1>
        <charts v-if="'tab3' === tabItem" :props="props" :data="data">tab3</charts>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import Vue from "Vue";
import charts from "@/components/charts";
export default {
  name: "index",
  components: {
      charts
  },
  data(){
      return {
        tabItem: "tab1",
        data: null,
        // 配置参数（以下是默认）
        props: {
          width: '100%',
          height:'300px'
        }
      }
  },
  created(){
    // setTimeout 模拟请求数据
    setTimeout(() => {
      this.data = {
        title: "ECharts 入门示例",
        xAxis: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
        series: [5, 20, 36, 10, 10, 20]
      }

      let temp = this.tabItem;
      this.tabItem = '';
      Vue.nextTick(() => {
        this.tabItem = temp;
      })
    }, 5000);

  },
  
};
</script>

<style>
</style>
