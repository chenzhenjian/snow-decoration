<template>
  <div class="mod-config">
    <el-form  :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-button @click="getDataList()">刷新</el-button>
        <el-button v-if="isAuth('tx:target:save')" type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button v-if="isAuth('tx:target:delete')" type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
      </el-form-item>
    </el-form>
    <el-row>
      <el-dropdown trigger="click" :hide-on-click="false" style="cursor: pointer;float: right">
          <span class="el-dropdown-link">
            <span style="font-size: 12px;color: #00a0e9">设置</span>
            <i class="el-icon-menu"></i>
            <i class="el-icon-caret-bottom"></i>
          </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>
            <el-checkbox style="display: block;" v-model="item.visible" v-for="item in allCustomColumnList" :key="item.prpo">{{ item.label }}</el-checkbox>
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </el-row>
    <elx-table
      :height="siteContentViewHeight"
      :custom-columns.sync="customColumns"
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      style="width: 100%;">
      <elx-table-column
        type="selection"
        header-align="left"
        align="left"
        width="50">
      </elx-table-column>
      <elx-table-column
        prop="deptName"
        header-align="left"
        align="left"
        width="150px"
        label="部门">
      </elx-table-column>
      <elx-table-column
        prop="year"
        width="100px"
        header-align="left"
        align="center"
        label="目标年份">
      </elx-table-column>
      <elx-table-column
        prop="contract1"
        header-align="left"
        align="left"
        width="90px"
        label="1月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract1}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract2"
        header-align="left"
        align="left"
        width="90px"
        label="2月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract2}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract3"
        header-align="left"
        align="left"
        width="90px"
        label="3月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract3}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract4"
        header-align="left"
        align="left"
        width="90px"
        label="4月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract4}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract5"
        header-align="left"
        align="left"
        width="90px"
        label="5月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract5}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract6"
        header-align="left"
        align="left"
        width="90px"
        label="6月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract6}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract7"
        header-align="left"
        align="left"
        width="90px"
        label="7月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract7}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract8"
        header-align="left"
        align="left"
        width="90px"
        label="8月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract8}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract9"
        header-align="left"
        align="left"
        width="90px"
        label="9月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract9}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract10"
        header-align="left"
        align="left"
        width="95px"
        label="10月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract10}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract11"
        header-align="left"
        align="left"
        width="95px"
        label="11月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract11}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="contract12"
        header-align="left"
        align="left"
        width="95px"
        label="12月合同目标">
        <template slot-scope="scope">
          <span>{{scope.row.contract12}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal1"
        header-align="left"
        align="left"
        width="90px"
        label="1月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal1}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal2"
        header-align="left"
        align="left"
        width="90px"
        label="2月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal2}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal3"
        header-align="left"
        align="left"
        width="90px"
        label="3月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal3}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal4"
        header-align="left"
        align="left"
        width="90px"
        label="4月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal4}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal5"
        header-align="left"
        align="left"
        width="90px"
        label="5月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal5}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal6"
        header-align="left"
        align="left"
        width="90px"
        label="6月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal6}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal7"
        header-align="left"
        align="left"
        width="90px"
        label="7月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal7}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal8"
        header-align="left"
        align="left"
        width="90px"
        label="8月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal8}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal9"
        header-align="left"
        align="left"
        width="90px"
        label="9月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal9}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal10"
        header-align="left"
        align="left"
        width="95px"
        label="10月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal10}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal11"
        header-align="left"
        align="left"
        width="95px"
        label="11月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal11}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        prop="goal12"
        header-align="left"
        align="left"
        width="95px"
        label="12月收款目标">
        <template slot-scope="scope">
          <span>{{scope.row.goal12}}</span>
          <span>万元</span>
        </template>
      </elx-table-column>
      <elx-table-column
        fixed="right"
        header-align="left"
        align="left"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="addOrUpdateHandle(scope.row.id)">修改</el-button>
          <el-button type="text" size="small" @click="deleteHandle(scope.row.id)">删除</el-button>
        </template>
      </elx-table-column>
    </elx-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper">
    </el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
  </div>
</template>

<script>
  import AddOrUpdate from './target-add-or-update'
  export default {
    computed: {
      allCustomColumnList () {
        return this.customColumns.filter(item => item.prop)
      },
      siteContentViewHeight () {
        return this.$store.state.common.documentClientHeight - 230
      }
    },
    data () {
      return {
        dataList: [],
        pageIndex: 1,
        pageSize: 10,
        totalPage: 0,
        dataListLoading: false,
        dataListSelections: [],
        addOrUpdateVisible: false,
        dataForm: {},
        customColumns: []
      }
    },
    components: {
      AddOrUpdate
    },
    activated () {
      this.getDataList()
    },
    methods: {
      // 获取数据列表
      getDataList () {
        this.dataListLoading = true
        this.$http({
          url: this.$http.adornUrl('/tx/target/list'),
          method: 'get',
          params: this.$http.adornParams({
            'page': this.pageIndex,
            'limit': this.pageSize
          })
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.dataList = data.page.list
            this.totalPage = data.page.totalCount
          } else {
            this.dataList = []
            this.totalPage = 0
          }
          this.dataListLoading = false
        })
      },
      // 每页数
      sizeChangeHandle (val) {
        this.pageSize = val
        this.pageIndex = 1
        this.getDataList()
      },
      // 当前页
      currentChangeHandle (val) {
        this.pageIndex = val
        this.getDataList()
      },
      // 多选
      selectionChangeHandle (val) {
        this.dataListSelections = val
      },
      // 新增 / 修改
      addOrUpdateHandle (id) {
        this.addOrUpdateVisible = true
        this.$nextTick(() => {
          this.$refs.addOrUpdate.init(id)
        })
      },
      // 删除
      deleteHandle (id) {
        var ids = id ? [id] : this.dataListSelections.map(item => {
          return item.id
        })
        this.$confirm('确定要删除吗?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$http({
            url: this.$http.adornUrl('/tx/target/delete'),
            method: 'post',
            data: this.$http.adornData(ids, false)
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.$message({
                message: '操作成功',
                type: 'success',
                duration: 500,
                onClose: () => {
                  this.getDataList()
                }
              })
            } else {
              this.$message.error(data.msg)
            }
          })
        })
      }
    }
  }
</script>
