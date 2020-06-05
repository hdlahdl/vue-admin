<template>
  <div class="hello">
    <el-dialog title="编辑用户信息" :visible.sync="dialogEdit.show">
      <el-form :model="form" ref="formEdit" label-width="100px" :rules="formrules">
        <el-form-item label="日期" prop="date">
            <el-date-picker
              v-model="form.date"
              type="date"
              value-format="yyyy-MM-dd"
              style="width: 100%;"
              placeholder="选择日期">
            </el-date-picker>
        </el-form-item>
        <el-form-item label="姓名" prop="name">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" prop="email">
          <el-input v-model="form.email"></el-input>
        </el-form-item>
        <el-form-item label="标题" prop="title">
          <el-input v-model="form.title"></el-input>
        </el-form-item>
        <el-form-item label="评价" prop="evaluate">
          <el-input v-model="form.evaluate"></el-input>
        </el-form-item>
        <el-form-item label="状态" prop="state">
          <el-input v-model="form.state"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogEdit.show = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormEdit('formEdit')">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  name: 'EditUser',
  props: {
    dialogEdit: Object,
    form: Object
  },
  data () {
    return {
      forms: {
        date: '',
        name: '',
        email: '',
        title: '',
        evaluate: '',
        state: ''
      },
      formrules: {
        date: [{ required: true, message: '日期不能为空', trigger: 'blur' }],
        name: [{ required: true, message: '用户名不能为空', trigger: 'blur' }],
        email: [{ required: true, message: '邮箱不能为空', trigger: 'blur' }]
      }
    }
  },
  methods: {
    dialogFormEdit (formEdit) {
      this.$refs[formEdit].validate((valid) => {
        if (valid) {
          this.$emit('datas', this.form)
          console.log(this.form)
          this.dialogEdit.show = false
          this.form = {}
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>
