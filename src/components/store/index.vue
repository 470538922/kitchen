<template>
  <div class="store_list">
    <div class="top_list">
      <el-button
        size="small"
        type="primary"
        class="el-icon-circle-plus-outline"
      >添加商品</el-button>
    </div>
    <div class="bottom_list">
      <div class="top_title">
        <h4>商品列表</h4>
        <div class="top_search">
          <el-col
            :span="9"
            style="padding:0 5px;"
          >
            <el-select
              v-model="value"
              placeholder="请选择"
              size="small"
            >
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              >
              </el-option>
            </el-select>
          </el-col>
          <el-col
            :span="11"
            style="padding:0 5px;"
          >
            <el-input
              size="small"
              style="width:100%;"
              placeholder=""
            ></el-input>
          </el-col>
          <el-col
            :span="4"
            style="padding:0 5px;"
          >
            <el-button size="small">搜索</el-button>
          </el-col>
        </div>
      </div>
      <div class="table_list">
        <el-table
          :data="tableData"
          style="width: 100%"
          size="small"
          stripe
          tooltip-effect="light"
          :header-cell-style="{'background-color':'#eee','color':'#333333', 'font-weight': 'normal'}"
        >
          <el-table-column
            type="selection"
            width="30"
          >
          </el-table-column>
          <el-table-column
            label="名称"
            min-width="100"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <span>{{ scope.row.name }}</span>
            </template>
          </el-table-column>
          <el-table-column
            label="分类"
            min-width="60"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <span>{{ scope.row.classify }}</span>
            </template>
          </el-table-column>
          <el-table-column
            label="单价（元）"
            min-width="100"
          >
            <template slot-scope="scope">
              ￥<el-input
                size="small"
                type="number"
                v-model="scope.row.price"
                style="width:60px;padding:0;"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column
            label="库存"
            min-width="80"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <span>{{ scope.row.inventory }}</span>
            </template>
          </el-table-column>
          <el-table-column
            label="烹饪时长(分钟)"
            min-width="110"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <el-input
                size="small"
                type="number"
                v-model="scope.row.time"
                style="width:60px;padding:0;"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column
            label="净含量"
            min-width="100"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <span>{{ scope.row.content}}</span>
            </template>
          </el-table-column>
          <el-table-column
            label="上架"
            min-width="60"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <div @click.stop.prevent="changeUp(scope.$index, scope.row)">
                <i
                  class="iconfont"
                  v-if="scope.row.up==='0'"
                  style="color:green;cursor: pointer;"
                >&#xe659;</i>
                <i
                  class="iconfont"
                  v-if="scope.row.up==='1'"
                  style="color:red;cursor: pointer;"
                >&#xe658;</i>
              </div>

            </template>
          </el-table-column>
          <el-table-column
            label="新品"
            min-width="60"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <div @click.stop.prevent="changeNew(scope.$index, scope.row)">
                <i
                  class="iconfont"
                  v-if="scope.row.new==='0'"
                  style="color:green;cursor: pointer;"
                >&#xe659;</i>
                <i
                  class="iconfont"
                  v-if="scope.row.new==='1'"
                  style="color:red;cursor: pointer;"
                >&#xe658;</i>
              </div>

            </template>
          </el-table-column>
          <el-table-column
            label="热销"
            min-width="60"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <div @click.stop.prevent="changeHot(scope.$index, scope.row)">
                <i
                  class="iconfont"
                  v-if="scope.row.hot==='0'"
                  style="color:green;cursor: pointer;"
                >&#xe659;</i>
                <i
                  class="iconfont"
                  v-if="scope.row.hot==='1'"
                  style="color:red;cursor: pointer;"
                >&#xe658;</i>
              </div>

            </template>
          </el-table-column>
          <el-table-column
            label="排序"
            min-width="80"
            show-overflow-tooltip
          >
            <template slot-scope="scope">
              <el-input
                size="small"
                type="number"
                v-model="scope.row.sort"
                style="width:60px;padding:0;"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column
            label="操作"
            min-width="150"
          >
            <template slot-scope="scope">
              <el-button
                type="text"
                size="mini"
                @click="handleDetails(scope.$index, scope.row)"
              >查看</el-button>
              <el-button
                type="text"
                size="mini"
                @click="handleEdit(scope.$index, scope.row)"
              >修改</el-button>
              <el-button
                type="text"
                size="mini"
                @click="handleDelete(scope.$index, scope.row)"
              >删除</el-button>
            </template>
          </el-table-column>
        </el-table>

      </div>
      <div
        class="block"
        style="margin-top:10px;float:right"
      >
        <el-pagination
          background
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page.sync="currentPage"
          :page-sizes="[15, 30, 100]"
          :page-size="100"
          layout="sizes, prev, pager, next"
          :total="1000"
        >
        </el-pagination>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      currentPage:1,
      value: "",
      options: [
        {
          label: "炒菜",
          value: "炒菜"
        },
        {
          label: "炖菜",
          value: "炖菜"
        },
        {
          label: "盐焗",
          value: "盐焗"
        },
        {
          label: "清蒸",
          value: "清蒸"
        },
        {
          label: "红烧",
          value: "红烧"
        }
      ],
      tableData: [
        {
          name: "素炒花菜",
          price: "9.8",
          classify: "素菜",
          inventory: "10",
          time: "5",
          content: "400克",
          up: "0",
          new: "0",
          hot: "1",
          sort: "100"
        }
      ]
    };
  },
  methods: {
    handleDetails(index, rowData) {
      let params = { type: "detalis", index: index, rowData: rowData };
      console.log(params);
    },
    handleEdit(index, rowData) {
      let params = { type: "edit", index: index, rowData: rowData };
      console.log(params);
    },
    handleDelete(index, rowData) {
      let params = { type: "delete", index: index, rowData: rowData };
      console.log(params);
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
    changeNew(index, val) {
      console.log(val.new);
      if (val.new === "1") {
        this.tableData[index].new = "0";
      } else {
        this.tableData[index].new = "1";
      }
    },
    changeUp(index, val) {
      console.log(val.new);
      if (val.up === "1") {
        this.tableData[index].up = "0";
      } else {
        this.tableData[index].up = "1";
      }
    },
    changeHot(index, val) {
      console.log(val.new);
      if (val.hot === "1") {
        this.tableData[index].hot = "0";
      } else {
        this.tableData[index].hot = "1";
      }
    }
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
.store_list {
  font-size: 14px;
  color: @font-normal;
  .top_list {
    // line-height: 60px;
    background-color: white;
    padding: 10px;
  }
  .bottom_list {
    background-color: white;
    margin-top: 10px;
    padding-bottom: 10px;
    overflow: hidden;
    .top_title {
      padding: 0 10px;
      line-height: 60px;
      overflow: hidden;
      border-bottom: @border;
      h4 {
        float: left;
      }
      .top_search {
        width: 400px;
        float: right;
      }
    }
    .table_list {
      overflow: hidden;
      padding: 10px;
      .el-input__inner {
        padding: 0;
        border: none;
        &:focus {
          border: 1px solid #1cc09f;
        }
      }
    }
  }
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
  }
  input[type="number"] {
    -moz-appearance: textfield;
  }
}
</style>

