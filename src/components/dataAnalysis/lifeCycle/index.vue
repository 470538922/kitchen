<template>
  <div class="life_cycle">
    <div class="top_case">
      <ul>
        <li v-for="(item, index) in topValue" :key="index">
          <span class="labe_style">{{item.label}}：</span>
          <span class="value_style">{{item.value}}</span>
        </li>
      </ul>
    </div>
    <div class="center_case">
      <el-col :span="16">
        <el-table
          :data="tableData"
          @row-click="(row, column, event)=>rowClick(row, column, event)"
          :highlight-current-row="true"
          style="width: 100%"
          :height="366"
        >
          <el-table-column prop="name" label="产品名称" min-width="200"></el-table-column>
          <el-table-column prop="cate" label="产品分类" min-width="100"></el-table-column>
          <el-table-column prop="count" label="绑定数量" min-width="100"></el-table-column>
          <el-table-column prop="enterprise" label="接入厂商" min-width="200"></el-table-column>
          <el-table-column prop="desc" label="产品描述" min-width="200"></el-table-column>
          <el-table-column prop="time" label="接入时间" min-width="140"></el-table-column>
        </el-table>
      </el-col>
      <el-col :span="8">
        <div id="pie" ref="pie" style="width:100%;height:365px;"></div>
      </el-col>
    </div>
    <div class="bottom_case" ref="axis" style="width:100%;height:400px;"></div>
  </div>
</template>
<script>
var echarts = require("echarts");
export default {
  data() {
    return {
      tableData: [
        {
          id: 1,
          name: "长虹炒菜机",
          cate: "炒菜机器人",
          count: 128,
          enterprise: "长虹i厨",
          desc: "专业的炒菜机器人",
          time: "2019/1/23 15:27:11"
        },
        {
          id: 2,
          name: "长虹洗碗机",
          cate: "洗碗机",
          count: 89,
          enterprise: "长虹i厨",
          desc: "长虹智能洗碗机",
          time: "2019/3/26 12:30:46"
        },
        {
          id: 3,
          name: "长虹电饭煲",
          cate: "电饭煲",
          count: 73,
          enterprise: "长虹i厨",
          desc: "长虹智能电饭煲",
          time: "2019/5/17 18:27:11"
        },
        {
          id: 4,
          name: "长虹微波炉",
          cate: "微波炉",
          count: 91,
          enterprise: "长虹i厨",
          desc: "长虹智能微波炉",
          time: "2019/6/25 09:37:31"
        },
        {
          id: 5,
          name: "长虹压力锅",
          cate: "压力锅",
          count: 88,
          enterprise: "长虹i厨",
          desc: "长虹智能压力锅",
          time: "2019/6/29 15:15:18"
        }
      ],
      topValue: [
        { label: "绑定数", value: 290 },
        { label: "在线数", value: 279 },
        { label: "离线数", value: 11 },
        { label: "空闲数", value: 138 },
        { label: "使用数", value: 138 },
        { label: "故障数", value: 3 }
      ],
      pidData: [
        {
          type: 1,
          data: [
            {
              name: "绑定",
              value: 128
            },
            {
              name: "未绑定",
              value: 55
            }
          ]
        },
        {
          type: 2,
          data: [
            {
              name: "绑定",
              value: 89
            },
            {
              name: "未绑定",
              value: 17
            }
          ]
        },
        {
          type: 3,
          data: [
            {
              name: "绑定",
              value: 73
            },
            {
              name: "未绑定",
              value: 23
            }
          ]
        },
        {
          type: 4,
          data: [
            {
              name: "绑定",
              value: 91
            },
            {
              name: "未绑定",
              value: 35
            }
          ]
        },
        {
          type: 5,
          data: [
            {
              name: "绑定",
              value: 88
            },
            {
              name: "未绑定",
              value: 41
            }
          ]
        }
      ],
      getDateValue: [],
      axisData: [
        {
          id: 1,
          online: [
            52,
            68,
            85,
            88,
            92,
            75,
            70,
            65,
            73,
            77,
            83,
            89,
            92,
            97,
            99,
            90,
            86,
            70,
            85,
            91,
            98,
            111,
            115,
            105,
            98,
            93,
            105,
            111,
            117,
            121
          ],
          use: [
            41,
            53,
            77,
            63,
            85,
            65,
            60,
            55,
            63,
            67,
            63,
            79,
            82,
            87,
            79,
            80,
            76,
            60,
            75,
            81,
            88,
            101,
            105,
            95,
            88,
            83,
            95,
            101,
            107,
            111
          ],
          fault: [
            1,
            1,
            1,
            1,
            1,
            2,
            3,
            1,
            1,
            1,
            1,
            1,
            2,
            2,
            2,
            1,
            1,
            1,
            1,
            1,
            2,
            3,
            2,
            1,
            1,
            1,
            1,
            1,
            4,
            2
          ]
        },
        {
          id: 2,
          online: [
            32,
            48,
            55,
            58,
            62,
            57,
            52,
            45,
            51,
            57,
            60,
            62,
            65,
            68,
            70,
            60,
            65,
            63,
            57,
            52,
            50,
            53,
            59,
            63,
            69,
            65,
            66,
            72,
            80,
            87
          ],
          use: [
            28,
            38,
            45,
            58,
            56,
            47,
            42,
            35,
            41,
            47,
            48,
            51,
            54,
            55,
            49,
            50,
            55,
            53,
            47,
            42,
            40,
            43,
            49,
            60,
            59,
            55,
            56,
            62,
            70,
            77
          ],
          fault: [
            0,
            0,
            0,
            0,
            0,
            1,
            2,
            0,
            0,
            0,
            0,
            0,
            1,
            1,
            1,
            0,
            0,
            0,
            0,
            0,
            1,
            2,
            1,
            0,
            0,
            0,
            0,
            0,
            3,
            1
          ]
        },
        {
          id: 3,
          online: [
            22,
            25,
            28,
            33,
            38,
            35,
            32,
            34,
            39,
            42,
            43,
            47,
            50,
            52,
            56,
            58,
            52,
            57,
            55,
            60,
            55,
            60,
            65,
            62,
            58,
            59,
            63,
            65,
            69,
            71
          ],
          use: [
            11,
            15,
            14,
            22,
            19,
            17,
            16,
            17,
            20,
            25,
            24,
            29,
            25,
            21,
            28,
            33,
            37,
            40,
            42,
            46,
            48,
            42,
            47,
            44,
            50,
            45,
            30,
            38,
            31,
            59,
            49,
            53,
            55,
            59,
            61
          ],
          fault: [
            0,
            0,
            0,
            0,
            1,
            1,
            1,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            2,
            0,
            0,
            0,
            0,
            1,
            0,
            1,
            0,
            0,
            0,
            0,
            1,
            0,
            0
          ]
        },
        {
          id: 4,
          online: [
            22,
            25,
            38,
            33,
            38,
            35,
            32,
            34,
            39,
            42,
            43,
            47,
            30,
            52,
            56,
            68,
            52,
            57,
            55,
            70,
            55,
            60,
            65,
            62,
            68,
            59,
            63,
            65,
            69,
            81
          ],
          use: [
            11,
            15,
            24,
            22,
            19,
            17,
            16,
            17,
            20,
            25,
            24,
            29,
            15,
            21,
            28,
            43,
            37,
            40,
            42,
            56,
            48,
            42,
            47,
            44,
            60,
            45,
            30,
            38,
            31,
            59,
            49,
            53,
            55,
            59,
            71
          ],
          fault: [
            0,
            1,
            0,
            0,
            1,
            0,
            1,
            0,
            2,
            0,
            1,
            0,
            4,
            0,
            1,
            2,
            0,
            0,
            0,
            0,
            1,
            0,
            1,
            0,
            0,
            1,
            0,
            1,
            0,
            0
          ]
        },
        {
          id: 5,
          online: [
            22,
            25,
            28,
            33,
            48,
            35,
            32,
            34,
            39,
            42,
            53,
            40,
            50,
            52,
            56,
            68,
            52,
            57,
            55,
            60,
            55,
            60,
            55,
            62,
            58,
            59,
            63,
            65,
            69,
            71
          ],
          use: [
            11,
            15,
            14,
            22,
            29,
            17,
            16,
            17,
            20,
            25,
            34,
            20,
            25,
            21,
            28,
            43,
            37,
            40,
            42,
            46,
            48,
            42,
            37,
            44,
            50,
            45,
            30,
            38,
            31,
            59,
            49,
            53,
            55,
            59,
            61
          ],
          fault: [
            1,
            0,
            0,
            0,
            0,
            2,
            0,
            0,
            0,
            0,
            1,
            2,
            3,
            0,
            0,
            0,
            1,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            1,
            0,
            1,
            1,
            0
          ]
        }
      ]
    };
  },
  methods: {
    rowClick(row, column, event) {
      if (row.id == 1) {
        this.pieFunction(this.pidData[0]);
        this.axisFunction(this.axisData[0]);
      }
      if (row.id == 2) {
        this.pieFunction(this.pidData[1]);
        this.axisFunction(this.axisData[1]);
      }
      if (row.id == 3) {
        this.pieFunction(this.pidData[2]);
        this.axisFunction(this.axisData[2]);
      }
      if (row.id == 4) {
        this.pieFunction(this.pidData[3]);
        this.axisFunction(this.axisData[3]);
      }
      if (row.id == 5) {
        this.pieFunction(this.pidData[4]);
        this.axisFunction(this.axisData[4]);
      }
    },
    pieFunction(value) {
      console.log(value);
      let myPie = echarts.init(this.$refs.pie, "light");
      // let myPie = this.$refs.pie;
      let option = {
        backgroundColor: "#ffffff",
        title: {
          text: value.name,
          x: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: ["绑定", "未绑定"]
        },
        series: [
          {
            name: "是否绑定",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: value.data,
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
    yugi() {
      var d = new Date();
      for (let i = 2; i < 31; i++) {
        var month;
        var r = d.getDate() - 1;
        d.setDate(Math.abs(r));
        var day = d.getDate() < 10 ? "0" + d.getDate() : d.getDate();
        r < 0
          ? (month = d.getMonth() < 10 ? "0" + d.getMonth() : d.getMonth())
          : (month =
              d.getMonth() + 1 < 10
                ? "0" + parseInt(d.getMonth() + 1)
                : d.getMonth() + 1);
        var year = new Date().getFullYear();
        this.getDateValue.push(month + "/" + day);
      }
      this.getDateValue = this.getDateValue.reverse();
    },
    axisFunction(value) {
      let myPie = echarts.init(this.$refs.axis, "light");
      let option = {
        backgroundColor: "#ffffff",
        title: {},
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
          data: ["待机量", "使用量", "故障量"]
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
            data: this.getDateValue
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            name: "待机量",
            type: "line",
            label: {
              normal: {
                show: true,
                position: "top"
              }
            },
            data: value.online
          },
          {
            name: "使用量",
            type: "line",
            label: {
              normal: {
                show: true,
                position: "top"
              }
            },
            data: value.use
          },
          {
            name: "故障量",
            label: {
              normal: {
                show: true,
                position: "top"
              }
            },
            type: "line",
            data: value.fault
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
    this.pieFunction(this.pidData[0]);
    this.axisFunction(this.axisData[0]);
    // var yugi = function(n){ var now = new Date; now.setDate(now.getDate() - n); return now;}console.log(yugi(10))
  },
  created() {
    this.yugi();
  }
};
</script>
<style lang="less">
@main-color: #1cc09f;
@bgColor: #f0f2f5;
@font-normal: #333333;
@font-subsidiary: #999999;
@font-special: #1cc09f;
@border: 1px solid #dde2eb;
.life_cycle {
  .top_case {
    overflow: hidden;

    ul {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      li {
        background-color: white;
        list-style-type: none;
        display: inline-block;
        width: 16%;
        border: @border;
        line-height: 50px;
        // text-align: center;
        border-radius: 4px;
        span {
          display: inline-block;
        }
        .labe_style {
          width: 50%;
          text-align: right;
        }
        .value_style {
          font-family: Roboto;
          font-size: 18px;
          font-weight: 600;
        }
      }
    }
  }
  .center_case {
    overflow: hidden;
    padding-top: 30px;
  }
}
</style>