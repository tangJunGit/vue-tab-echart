<template>
  <div>
    <el-tabs v-model="tabItem" @tab-click="tabClick">
      <el-tab-pane label="tab1" name="tab1">
        <h1>tab1</h1>
        <charts v-if="'tab1' === tabItem" :height="height" :data="data">tab1</charts>
      </el-tab-pane>
      <el-tab-pane label="tab2" name="tab2">
        <h1>tab2</h1>
        <charts v-if="'tab2' === tabItem" :height="height" :data="data">tab2</charts>
      </el-tab-pane>
      <el-tab-pane label="tab3" name="tab3">
        <h1>tab3</h1>
        <charts v-if="'tab3' === tabItem" :height="height" title="echart 标题" :data="data">tab3</charts>
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
        data: [],
        height:'300px'
      }
  },
  created(){
    this.tabClick();
  },
  methods: {
    tabClick(){
      // setTimeout 模拟请求数据
      setTimeout(() => {
        this.data = [
            {name: '衬衫', value: 125},
            {name: '羊毛衫', value: 86},
            {name: '雪纺衫', value: 256},
            {name: '裤子', value: 345},
            {name: '高跟鞋', value: 45},
          ]
      }, 5000);
      
    },
  }
  
};
</script>

<style>
</style>
