<template>
  <div class="menu_analysis">
    <div class="top_case">
      <el-col :span="12">
        <div ref="axis1" style="width:100%;height:400px"></div>
      </el-col>
      <el-col :span="12">
        <div ref="pie1" style="width:100%;height:400px"></div>
      </el-col>
    </div>
    <div class="center_case">
      <el-col :span="12">
        <div ref="axis3" style="width:100%;height:400px"></div>
      </el-col>
      <el-col :span="12">
        <div ref="axis2" style="width:100%;height:400px"></div>
      </el-col>
    </div>
    <div class="pie_case">
      <el-col :span="8">
        <div ref="pie2" style="width:100%;height:400px"></div>
      </el-col>
      <el-col :span="8">
        <div ref="pie3" style="width:100%;height:400px"></div>
      </el-col>
      <el-col :span="8">
        <div ref="pie4" style="width:100%;height:400px"></div>
      </el-col>
    </div>
    <div class="bottom_case">
      <el-col :span="24">
        <div ref="axis4" style="width:100%;height:400px"></div>
      </el-col>
    </div>
  </div>
</template>
<script>
var echarts = require("echarts");
export default {
  data() {
    return {};
  },
  methods: {
    axis1() {
      let myPie = echarts.init(this.$refs.axis1, "light");
      let option = {
        title: {
          text: "年龄分布",
          x: "center"
        },
        backgroundColor: "#ffffff",
        color: ["#3398DB"],
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
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
            data: ["19岁以下", "20-29岁", "30-39岁", "40-49岁", "50岁以上"],
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            type: "bar",
            barWidth: "50px",
            name: "数量",
            data: [497, 2498, 1892, 1478, 307]
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    pieFunction(value) {
      let myPie = echarts.init(this.$refs.pie1, "light");
      // let myPie = this.$refs.pie;
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "用户性别占比",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: ["男性", "女性"]
        },
        series: [
          {
            name: "性别",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [{ value: 1729, name: "女性" }, { value: 763, name: "男性" }],
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
    axis2() {
      let myPie = echarts.init(this.$refs.axis2, "light");
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "近一周菜谱烹饪",
          x: "left"
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        legend: {
          data: [
            "回锅肉",
            "京酱肉丝",
            "青椒肉丝",
            "宫保鸡丁",
            "水煮肉片",
            "酸菜鱼",
            "其他"
          ]
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
            data: ["周一", "周二", "周三", "周四", "周五", "周六", "周日"]
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            name: "回锅肉",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [300, 320, 350, 260, 390, 330, 320]
          },
          {
            name: "京酱肉丝",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: "青椒肉丝",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: "宫保鸡丁",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [150, 232, 201, 154, 190, 330, 410]
          },
          {
            name: "水煮肉片",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [230, 250, 200, 100, 120, 300, 300]
          },
          {
            name: "酸菜鱼",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [120, 132, 101, 134, 290, 230, 220]
          },
          {
            name: "其他",
            type: "bar",
            stack: "菜谱",
            barWidth: "50px",
            data: [700, 750, 730, 760, 690, 1000, 1200]
          }
        ]
      };
      myPie.setOption(option);
      window.onresize = function() {
        myPie.resize();
      };
    },
    axis3() {
      let myPie = echarts.init(this.$refs.axis3, "light");
      let option = {
        title: {
          text: "菜谱热销榜",
          x: "center"
        },
        backgroundColor: "#ffffff",
        color: ["#3398DB"],
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
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
            data: [
              "盐煎肉",
              "鱼香肉丝",
              "干煸四季豆",
              "回锅肉",
              "酸菜鱼",
              "宫保鸡丁",
              "辣子鸡",
              "口水鸡",
              "麻婆豆腐",
              "蚂蚁上树",
              "水煮肉片"
            ],
            axisLabel: {
              rotate: 60
            },
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            type: "bar",
            name: "销量",
            data: [875, 789, 740, 570, 452, 379, 330, 289, 216, 178, 150]
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
          text: "用户城市分布",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: [
            "成都",
            "重庆",
            "北京",
            "上海",
            "广州",
            "深圳",
            "郑州",
            "江苏",
            "南京",
            "其他"
          ]
        },
        series: [
          {
            name: "地区",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [
              { value: 1548, name: "成都" },
              { value: 1302, name: "重庆" },
              { value: 1000, name: "北京" },
              { value: 975, name: "上海" },
              { value: 800, name: "广州" },
              { value: 500, name: "深圳" },
              { value: 650, name: "郑州" },
              { value: 340, name: "江苏" },
              { value: 200, name: "南京" },
              { value: 2300, name: "其他" }
            ],
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
          text: "用户口味占比",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: ["不辣", "微辣", "中辣", "特辣"]
        },
        series: [
          {
            name: "口味",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [
              { value: 290, name: "不辣" },
              { value: 650, name: "微辣" },
              { value: 500, name: "中辣" },
              { value: 190, name: "特辣" }
            ],
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
          text: "用户最爱菜谱分类占比",
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: ["快手菜", "下饭菜", "家常菜", "素菜", "肉菜", "汤品", "其他"]
        },
        series: [
          {
            name: "性别",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [
              { value: 602, name: "快手菜" },
              { value: 1302, name: "下饭菜" },
              { value: 1589, name: "家常菜" },
              { value: 890, name: "素菜" },
              { value: 1020, name: "肉菜" },
              { value: 500, name: "汤品" },
              { value: 650, name: "其他" }
            ],
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
    axis4() {
      let myPie = echarts.init(this.$refs.axis4, "light");
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: "每月用户喜爱菜谱",
          x: "left"
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        legend: {
          data: [
            "回锅肉",
            "京酱肉丝",
            "青椒肉丝",
            "宫保鸡丁",
            "水煮肉片",
            "酸菜鱼",
            "其他"
          ]
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
            name: "回锅肉",
            type: "bar",
            stack: "菜谱",
            data: [300, 320, 350, 260, 390, 330, 320, 300, 320, 350, 260, 390]
          },
          {
            name: "京酱肉丝",
            type: "bar",
            stack: "菜谱",
            data: [120, 132, 101, 134, 90, 230, 210, 101, 134, 90, 230, 210]
          },
          {
            name: "青椒肉丝",
            type: "bar",
            stack: "菜谱",
            data: [220, 182, 191, 234, 290, 330, 310, 101, 134, 90, 230, 210]
          },
          {
            name: "宫保鸡丁",
            type: "bar",
            stack: "菜谱",
            data: [150, 232, 201, 154, 190, 330, 410, 230, 250, 200, 100, 120]
          },
          {
            name: "水煮肉片",
            type: "bar",
            stack: "菜谱",
            data: [230, 250, 200, 100, 120, 300, 300, 120, 132, 101, 134, 290]
          },
          {
            name: "酸菜鱼",
            type: "bar",
            stack: "菜谱",
            data: [120, 132, 101, 134, 290, 230, 220, 191, 234, 290, 330, 310]
          },
          {
            name: "其他",
            type: "bar",
            stack: "菜谱",
            data: [
              700,
              750,
              730,
              760,
              690,
              1000,
              1200,
              750,
              730,
              760,
              690,
              1000
            ]
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
    this.axis1();
    this.axis2();
    this.axis3();
    this.pieFunction();
    this.pieFunction2();
    this.pieFunction3();
    this.pieFunction4();
    this.axis4();
  },
  created() {}
};
</script>
<style lang="less">
.menu_analysis {
  .top_case {
    overflow: hidden;
  }
  .center_case {
    overflow: hidden;
    margin-top: 12px;
  }
  .pie_case {
    overflow: hidden;
    margin-top: 12px;
  }
  .bottom_case {
    overflow: hidden;
    margin-top: 12px;
  }
}
</style>