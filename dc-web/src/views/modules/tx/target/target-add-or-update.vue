<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form inline :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="120px">
    <el-form-item label="部门" prop="deptId">
      <el-popover
        ref="deptListPopover"
        placement="bottom-start"
        trigger="click">
        <el-tree
          clearable
          :data="dataList"
          :props="deptListTreeProps"
          node-key="id"
          ref="deptListTree"
          @current-change="deptListTreeCurrentChangeHandle"
          :default-expand-all="true"
          :highlight-current="true"
          :expand-on-click-node="false">
        </el-tree>
      </el-popover>
      <el-input style="width: 236px" v-model="dataForm.deptName" v-popover:deptListPopover :readonly="true" placeholder="点击选择部门" class="menu-list__input"></el-input>
    </el-form-item>
    <el-form-item label="目标年份" prop="year">
      <el-date-picker style="width: 236px" type="year" placeholder="目标年份" v-model="dataForm.year"></el-date-picker>
    </el-form-item>
    <el-form-item class="el-input--mini" label="1月合同目标" prop="contract1">
      <el-input v-model="dataForm.contract1" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="2月合同目标" prop="contract2">
      <el-input v-model="dataForm.contract2" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="3月合同目标" prop="contract3">
      <el-input v-model="dataForm.contract3" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="4月合同目标" prop="contract4">
      <el-input v-model="dataForm.contract4" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="5月合同目标" prop="contract5">
      <el-input v-model="dataForm.contract5" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="6月合同目标" prop="contract6">
      <el-input v-model="dataForm.contract6" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="7月合同目标" prop="contract7">
      <el-input v-model="dataForm.contract7" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="8月合同目标" prop="contract8">
      <el-input v-model="dataForm.contract8" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="9月合同目标" prop="contract9">
      <el-input v-model="dataForm.contract9" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="10月合同目标" prop="contract10">
      <el-input v-model="dataForm.contract10" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="11月合同目标" prop="contract11">
      <el-input v-model="dataForm.contract11" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="12月合同目标" prop="contract12">
      <el-input v-model="dataForm.contract12" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="1月收款目标" prop="goal1">
      <el-input v-model="dataForm.goal1" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="2月收款目标" prop="goal2">
      <el-input v-model="dataForm.goal2" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="3月收款目标" prop="goal3">
      <el-input v-model="dataForm.goal3" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="4月收款目标" prop="goal4">
      <el-input v-model="dataForm.goal4" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="5月收款目标" prop="goal5">
      <el-input v-model="dataForm.goal5" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="6月收款目标" prop="goal6">
      <el-input v-model="dataForm.goal6" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="7月收款目标" prop="goal7">
      <el-input v-model="dataForm.goal7" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="8月收款目标" prop="goal8">
      <el-input v-model="dataForm.goal8" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="9月收款目标" prop="goal9">
      <el-input v-model="dataForm.goal9" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="10月收款目标" prop="goal10">
      <el-input v-model="dataForm.goal10" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="11月收款目标" prop="goal11">
      <el-input v-model="dataForm.goal11" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    <el-form-item class="el-input--mini" label="12月收款目标" prop="goal12">
      <el-input v-model="dataForm.goal12" v-bind:precision="2" type="number">
        <template slot="append">万元</template>
      </el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button  @click="visible = false">取消</el-button>
      <el-button  type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
  import {treeDataTranslate} from '@/utils/index'
  import * as Public from '../../../../js/api/public'
  export default {
    data () {
      return {
        visible: false,
        dataForm: {
          id: 0,
          deptId: '',
          deptName: '',
          year: new Date(),
          contract1: 0,
          contract2: 0,
          contract3: 0,
          contract4: 0,
          contract5: 0,
          contract6: 0,
          contract7: 0,
          contract8: 0,
          contract9: 0,
          contract10: 0,
          contract11: 0,
          contract12: 0,
          goal1: 0,
          goal2: 0,
          goal3: 0,
          goal4: 0,
          goal5: 0,
          goal6: 0,
          goal7: 0,
          goal8: 0,
          goal9: 0,
          goal10: 0,
          goal11: 0,
          goal12: 0
        },
        dataRule: {
          deptId: [
            { required: true, message: '部门不能为空', trigger: 'change' }
          ],
          year: [
            { required: true, message: '目标年份不能为空', trigger: 'blur' }
          ],
          contract1: [
            { required: true, message: '1月合同目标不能为空', trigger: 'blur' }
          ],
          contract2: [
            { required: true, message: '2月合同目标不能为空', trigger: 'blur' }
          ],
          contract3: [
            { required: true, message: '3月合同目标不能为空', trigger: 'blur' }
          ],
          contract4: [
            { required: true, message: '4月合同目标不能为空', trigger: 'blur' }
          ],
          contract5: [
            { required: true, message: '5月合同目标不能为空', trigger: 'blur' }
          ],
          contract6: [
            { required: true, message: '6月合同目标不能为空', trigger: 'blur' }
          ],
          contract7: [
            { required: true, message: '7月合同目标不能为空', trigger: 'blur' }
          ],
          contract8: [
            { required: true, message: '8月合同目标不能为空', trigger: 'blur' }
          ],
          contract9: [
            { required: true, message: '9月合同目标不能为空', trigger: 'blur' }
          ],
          contract10: [
            { required: true, message: '10月合同目标不能为空', trigger: 'blur' }
          ],
          contract11: [
            { required: true, message: '11月合同目标不能为空', trigger: 'blur' }
          ],
          contract12: [
            { required: true, message: '12月合同目标不能为空', trigger: 'blur' }
          ],
          goal1: [
            { required: true, message: '1月收款目标不能为空', trigger: 'blur' }
          ],
          goal2: [
            { required: true, message: '2月收款目标不能为空', trigger: 'blur' }
          ],
          goal3: [
            { required: true, message: '3月收款目标不能为空', trigger: 'blur' }
          ],
          goal4: [
            { required: true, message: '4月收款目标不能为空', trigger: 'blur' }
          ],
          goal5: [
            { required: true, message: '5月收款目标不能为空', trigger: 'blur' }
          ],
          goal6: [
            { required: true, message: '6月收款目标不能为空', trigger: 'blur' }
          ],
          goal7: [
            { required: true, message: '7月收款目标不能为空', trigger: 'blur' }
          ],
          goal8: [
            { required: true, message: '8月收款目标不能为空', trigger: 'blur' }
          ],
          goal9: [
            { required: true, message: '9月收款目标不能为空', trigger: 'blur' }
          ],
          goal10: [
            { required: true, message: '10月收款目标不能为空', trigger: 'blur' }
          ],
          goal11: [
            { required: true, message: '11月收款目标不能为空', trigger: 'blur' }
          ],
          goal12: [
            { required: true, message: '12月收款目标不能为空', trigger: 'blur' }
          ]
        },
        dataList: [],
        deptListTreeProps: {
          label: 'name',
          children: 'child'
        }
      }
    },
    methods: {
      // 菜单树选中
      deptListTreeCurrentChangeHandle (data, node) {
        this.dataForm.deptId = data.id
        this.dataForm.deptName = data.name
      },
      // 菜单树设置当前选中节点
      deptListTreeSetCurrentNode () {
        this.$refs.deptListTree.setCurrentKey(this.dataForm.deptId)
        this.dataForm.deptName = (this.$refs.deptListTree.getCurrentNode() || {})['name']
      },
      initPublic () {
        Public.findAllDept.r().then((res) => {
          if (res.data && res.data.code === 0) {
            this.dataList = treeDataTranslate(res.data.list, 'id')
          } else {
            this.dataList = []
          }
          this.dataListLoading = false
        })
      },
      init (id) {
        this.$nextTick(() => {
          this.initPublic()
        })
        this.dataForm.deptId = ''
        this.dataForm.deptName = ''
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/tx/target/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.deptId = data.target.deptId
                this.dataForm.deptName = data.target.deptName
                this.dataForm.year = data.target.year
                this.dataForm.contract1 = data.target.contract1
                this.dataForm.contract2 = data.target.contract2
                this.dataForm.contract3 = data.target.contract3
                this.dataForm.contract4 = data.target.contract4
                this.dataForm.contract5 = data.target.contract5
                this.dataForm.contract6 = data.target.contract6
                this.dataForm.contract7 = data.target.contract7
                this.dataForm.contract8 = data.target.contract8
                this.dataForm.contract9 = data.target.contract9
                this.dataForm.contract10 = data.target.contract10
                this.dataForm.contract11 = data.target.contract11
                this.dataForm.contract12 = data.target.contract12
                this.dataForm.goal1 = data.target.goal1
                this.dataForm.goal2 = data.target.goal2
                this.dataForm.goal3 = data.target.goal3
                this.dataForm.goal4 = data.target.goal4
                this.dataForm.goal5 = data.target.goal5
                this.dataForm.goal6 = data.target.goal6
                this.dataForm.goal7 = data.target.goal7
                this.dataForm.goal8 = data.target.goal8
                this.dataForm.goal9 = data.target.goal9
                this.dataForm.goal10 = data.target.goal10
                this.dataForm.goal11 = data.target.goal11
                this.dataForm.goal12 = data.target.goal12
              }
            })
          }
        })
      },
      // 表单提交
      dataFormSubmit () {
        this.$refs['dataForm'].validate((valid) => {
          if (valid) {
            this.$http({
              url: this.$http.adornUrl(`/tx/target/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'deptId': this.dataForm.deptId,
                'year': this.dataForm.year.getFullYear().toString(),
                'contract1': this.dataForm.contract1,
                'contract2': this.dataForm.contract2,
                'contract3': this.dataForm.contract3,
                'contract4': this.dataForm.contract4,
                'contract5': this.dataForm.contract5,
                'contract6': this.dataForm.contract6,
                'contract7': this.dataForm.contract7,
                'contract8': this.dataForm.contract8,
                'contract9': this.dataForm.contract9,
                'contract10': this.dataForm.contract10,
                'contract11': this.dataForm.contract11,
                'contract12': this.dataForm.contract12,
                'goal1': this.dataForm.goal1,
                'goal2': this.dataForm.goal2,
                'goal3': this.dataForm.goal3,
                'goal4': this.dataForm.goal4,
                'goal5': this.dataForm.goal5,
                'goal6': this.dataForm.goal6,
                'goal7': this.dataForm.goal7,
                'goal8': this.dataForm.goal8,
                'goal9': this.dataForm.goal9,
                'goal10': this.dataForm.goal10,
                'goal11': this.dataForm.goal11,
                'goal12': this.dataForm.goal12
              })
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.$message({
                  message: '操作成功',
                  type: 'success',
                  duration: 500,
                  onClose: () => {
                    this.visible = false
                    this.$emit('refreshDataList')
                  }
                })
              } else {
                this.$message.error(data.msg)
              }
            })
          }
        })
      }
    }
  }
</script>
<style lang="scss">
  .mod-menu {
    .menu-list__input,
    .icon-list__input {
      > .el-input__inner {
        cursor: pointer;
      }
    }
    &__icon-popover {
      max-width: 370px;
    }
    &__icon-list {
      max-height: 180px;
      padding: 0;
      margin: -8px 0 0 -8px;
      > .el-button {
        padding: 8px;
        margin: 8px 0 0 8px;
        > span {
          display: inline-block;
          vertical-align: middle;
          width: 18px;
          height: 18px;
          font-size: 18px;
        }
      }
    }
    .icon-list__tips {
      font-size: 18px;
      text-align: center;
      color: #e6a23c;
      cursor: pointer;
    }
  }
</style>
