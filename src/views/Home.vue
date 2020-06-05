<template>
<div class="content">
  <el-row :gutter="20">
  <el-col :span="8">
    <el-form :model="form" label-width="120px">
      <el-form-item style="float: left" label="查询用户信息:">
        <el-input v-model="keyUser" placeholder="查询所需要的内容......"></el-input>
      </el-form-item>
    </el-form>
  </el-col>
  <el-col :span="4">
    <el-button type="primary" size="medium" icon="el-icon-edit-outline" @click="hanldeAdd()">添加</el-button>
</el-col>
</el-row>
  <AddUser :dialogAdd="dialogAdd" @datas="change($event)"></AddUser>
  <EditUser :dialogEdit="dialogEdit" :form='form1' @datas="change2($event)"></EditUser>
  <el-table
    :data="searchUserinfo (keyUser)"
    highlight-current-row
    border
    style="width: 100%">
    <el-table-column
      fixed
      sortable
      prop="date"
      label="日期"
      width="150">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      width="120">
    </el-table-column>
    <el-table-column
      prop="email"
      label="邮箱"
      width="120">
    </el-table-column>
    <el-table-column
      prop="title"
      label="标题"
      width="120">
    </el-table-column>
    <el-table-column
      prop="evaluate"
      label="评价"
      width="300">
    </el-table-column>
    <el-table-column
      prop="state"
      label="状态"
      width="120">
    </el-table-column>
    <el-table-column
      fixed="right"
      label="操作"
      width="240">
      <template slot-scope="scope">
        <el-button @click="handleClick(scope.row)" size="small" type="success" >查看</el-button>
        <el-button size="small" type="primary" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-button size="small" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</div>
</template>

<script>
import AddUser from '@/components/add.vue'
import EditUser from '@/components/edit.vue'
export default {
  components: {
    AddUser,
    EditUser
  },
  methods: {
    handleClick (row) {
      console.log(row)
    },
    hanldeAdd () {
      this.dialogAdd.show = true
    },
    change (data) {
      console.log('11111')
      console.log(data)
      this.tableData.push(data)
    },
    change2 (data) {
      console.log('22222')
      console.log(data)
      this.tableData.splice(this.index, 1, data)
    },
    handleDelete (index, row) {
      this.tableData.splice(index, 1)
      this.$message({
        type: 'success',
        message: '删除信息成功'
      })
    },
    searchUserinfo (keyUser) {
      return this.tableData.filter((user) => {
        if (user.name.includes(keyUser)) {
          return user
        }
      })
    },
    handleEdit (index, row) {
      this.dialogEdit.show = true
      this.index = index
      this.form1 = {
        date: row.date,
        name: row.name,
        email: row.email,
        title: row.title,
        evaluate: row.evaluate,
        state: row.state
        // id: row.id
      }
    }
  },
  data () {
    return {
      form: {},
      keyUser: '',
      dialogAdd: {
        show: false
      },
      dialogEdit: {
        show: false
      },
      index: '',
      form1: {
        date: '',
        name: '',
        email: '',
        title: '',
        evaluate: '',
        state: ''
      },
      tableData: [{
        date: '2016-05-02',
        name: '王小虎1',
        email: '123@qq.com',
        title: '普陀区',
        evaluate: '上海市普陀区金沙江路 1518 弄',
        state: 200333
      }, {
        date: '2016-05-04',
        name: '王小虎2',
        email: '123@qq.com',
        title: '普陀区',
        evaluate: '上海市普陀区金沙江路 1518 弄',
        state: 200333
      }, {
        date: '2016-05-01',
        name: '王小虎3',
        email: '123@qq.com',
        title: '普陀区',
        evaluate: '上海市普陀区金沙江路 1518 弄',
        state: 200333
      }, {
        date: '2016-05-03',
        name: '王小虎4',
        email: '123@qq.com',
        title: '普陀区',
        evaluate: '上海市普陀区金沙江路 1518 弄',
        state: 200333
      }]
    }
  }
}
</script>
<style>
.content{
  padding-top: 20px;
}
</style>
