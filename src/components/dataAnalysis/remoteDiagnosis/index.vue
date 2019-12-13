<template>
  <div class="remote_diagnosis">
    <div class="top_case">
      <h4>故障</h4>
      <el-col :span="8">
        <el-table :data="tableData" size="small" style="width: 100%" :height="401">
          <el-table-column prop="code" label="故障编码" min-width="100"></el-table-column>
          <el-table-column prop="message" label="故障信息" min-width="140"></el-table-column>
          <el-table-column prop="num" label="数量" min-width="80"></el-table-column>
        </el-table>
      </el-col>
      <el-col :span="16">
        <el-col :span="12">
          <div ref="pie1" style="width:100%;height:400px"></div>
        </el-col>
        <el-col :span="12">
          <div ref="pie2" style="width:100%;height:400px"></div>
        </el-col>
      </el-col>
      <el-col :span="24">
        <div ref="axis1" style="width:100%;height:400px"></div>
      </el-col>
    </div>
    <div class="bottom_case">
      <h4>告警</h4>
      <el-col :span="8">
        <el-table :data="alarm" size="small" style="width: 100%" :height="401">
          <el-table-column prop="code" label="预警编码" min-width="100"></el-table-column>
          <el-table-column prop="message" label="预警信息" min-width="140"></el-table-column>
          <el-table-column prop="num" label="数量" min-width="80"></el-table-column>
        </el-table>
      </el-col>
      <el-col :span="16">
        <el-col :span="12">
          <div ref="pie3" style="width:100%;height:400px"></div>
        </el-col>
        <el-col :span="12">
          <div ref="pie4" style="width:100%;height:400px"></div>
        </el-col>
      </el-col>
      <el-col :span="24">
        <div ref="axis2" style="width:100%;height:400px"></div>
      </el-col>
    </div>
  </div>
</template>
<script>
var echarts = require("echarts");
export default {
  data() {
    return {
      tableData: [
        { code: "FDJ0821", message: "电机故障", num: 12 },
        { code: "FWd0dw", message: "加热线圈故障", num: 11 },
        { code: "Fdw0fsw", message: "温度传感器故障", num: 23 },
        { code: "FS0843f", message: "油泵故障", num: 4 }
      ],
      age: [
        { name: "40岁以上", value: 46 },
        { name: "30-40岁", value: 32 },
        { name: "30岁以下", value: 22 }
      ],
      faultData: [
        { name: "电机故障", value: 24 },
        { name: "加热线圈故障", value: 22 },
        { name: "温度传感器故障", value: 46 },
        { name: "油泵故障", value: 8 }
      ],
      alarm: [
        { code: "ADJ0821", message: "干烧预警", num: 15 },
        { code: "AWd0dw", message: "积水预警", num: 12 },
        { code: "Adw0fsw", message: "食物长时间未取出", num: 8 },
        { code: "AS0843f", message: "高温预警", num: 15 }
      ],
      alarmData: [
        { name: "干烧预警", value: 30 },
        { name: "积水预警", value: 24 },
        { name: "食物长时间未取出", value: 16 },
        { name: "高温预警", value: 30 }
      ]
    };
  },
  methods: {
    pieFunction1(value) {
      let myPie = echarts.init(this.$refs.pie1, "light");
      // let myPie = this.$refs.pie;
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "故障率数据",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: this.faultData.map(item => item.name)
        },
        series: [
          {
            name: "故障率",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: this.faultData,
            itemStyle: {
              emphasis: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    pieFunction2(value) {
      let myPie = echarts.init(this.$refs.pie2, "light");
      // let myPie = this.$refs.pie;
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "年龄分布数据",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: this.age.map(item => item.name)
        },
        series: [
          {
            name: "是否绑定",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: this.age,
            itemStyle: {
              emphasis: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    pieFunction3(value) {
      let myPie = echarts.init(this.$refs.pie3, "light");
      // let myPie = this.$refs.pie;
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "告警率数据",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: this.alarmData.map(item => item.name)
        },
        series: [
          {
            name: "故障率",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: this.alarmData,
            itemStyle: {
              emphasis: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    pieFunction4(value) {
      let myPie = echarts.init(this.$refs.pie4, "light");
      // let myPie = this.$refs.pie;
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "年龄分布数据",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: this.age.map(item => item.name)
        },
        series: [
          {
            name: "是否绑定",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: this.age,
            itemStyle: {
              emphasis: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    axis1() {
      let myPie = echarts.init(this.$refs.axis1, "light");
      let option = {
        backgroundColor: "#ffffff",
        title: { text: "每月故障数据折线图", x: "center" },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            label: {
              backgroundColor: "#6a7985"
            }
          }
        },
        legend: {
          data: []
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            data: [
              "一月",
              "二月",
              "三月",
              "四月",
              "五月",
              "六月",
              "七月",
              "八月",
              "九月",
              "十月",
              "十一月",
              "十二月"
            ]
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            name: "故障量",
            type: "line",
            label: {
              normal: {
                show: true,
                position: "top"
              }
            },
            data: [43, 23, 25, 25, 32, 29, 33, 28, 40, 31, 26, 41]
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    axis2() {
      let myPie = echarts.init(this.$refs.axis2, "light");
      let option = {
        backgroundColor: "#ffffff",
        title: { text: "每月告警数据折线图", x: "center" },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            label: {
              backgroundColor: "#6a7985"
            }
          }
        },
        legend: {
          data: []
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            data: [
              "一月",
              "二月",
              "三月",
              "四月",
              "五月",
              "六月",
              "七月",
              "八月",
              "九月",
              "十月",
              "十一月",
              "十二月"
            ]
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            name: "告警量",
            type: "line",
            label: {
              normal: {
                show: true,
                position: "top"
              }
            },
            data: [43, 23, 25, 25, 32, 29, 33, 28, 40, 31, 26, 41]
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    }
  },
  mounted() {
    this.pieFunction1();
    this.pieFunction2();
    this.pieFunction3();
    this.pieFunction4();
    this.axis1();
    this.axis2();
  },
  created() {}
};
</script>
<style lang="less">
.remote_diagnosis {
  .top_case {
    overflow: hidden;
    background-color: white;
    h4 {
      line-height: 40px;
      padding-left: 12px;
    }
  }
  .bottom_case {
    overflow: hidden;
    background-color: white;
    margin-top: 12px;
    h4 {
      line-height: 40px;
      padding-left: 12px;
    }
  }
}
</style>