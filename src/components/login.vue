<template>
  <div class="login">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="登录" name="first">
        <el-form
          :model="ruleForm1"
          status-icon
          :rules="rules1"
          ref="ruleForm1"
          label-width="100px"
          class="demo-ruleForm"
        >
          <el-form-item label="用户名" prop="username">
            <el-input v-model.number="ruleForm1.username"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="pass">
            <el-input type="password" v-model="ruleForm1.pass" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="login('ruleForm1')">提交</el-button>
            <el-button @click="resetForm('ruleForm1')">重置</el-button>
          </el-form-item>
        </el-form>
      </el-tab-pane>
      <el-tab-pane label="注册" name="second">
        <el-form
          :model="ruleForm2"
          status-icon
          :rules="rules2"
          ref="ruleForm2"
          label-width="100px"
          class="demo-ruleForm"
        >
          <el-form-item label="用户名" prop="username">
            <el-input v-model.number="ruleForm2.username"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="pass">
            <el-input type="password" v-model="ruleForm2.pass" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="确认密码" prop="checkPass">
            <el-input type="password" v-model="ruleForm2.checkPass" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="register('ruleForm2')">提交</el-button>
            <el-button @click="resetForm('ruleForm2')">重置</el-button>
          </el-form-item>
        </el-form>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    var checkUsername = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("用户名不能为空"));
      } else {
        callback();
      }
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm1.checkPass !== "") {
          this.$refs.ruleForm1.validateField("checkPass");
        }
        if (this.ruleForm2.checkPass !== "") {
          this.$refs.ruleForm2.validateField("checkPass");
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm2.pass) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    return {
      activeName: "first",
      ruleForm1: {
        pass: "",
        username: ""
      },
      ruleForm2: {
        pass: "",
        checkPass: "",
        username: ""
      },
      rules1: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        username: [{ validator: checkUsername, trigger: "blur" }]
      },
      rules2: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        checkPass: [{ validator: validatePass2, trigger: "blur" }],
        username: [{ validator: checkUsername, trigger: "blur" }]
      }
    };
  },
  methods: {
    login(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          axios
            .post("/proxyApi/user/login", {
              username: this.ruleForm1.username,
              password: this.ruleForm1.pass
            })
            .then(res => {
              if (res.code === 1) {
                this.$message({
                  message: "登录成功",
                  type: "success"
                });
                this.$router.push({name: home})
              } else {
                this.$message({
                  message: "登录失败",
                  type: "warning"
                });
              }
            }).catch(error => {
              console.log(error)
            });
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    register(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
         axios
            .post("/proxyApi/user/reg", {
              username: this.ruleForm2.username,
              password: this.ruleForm2.pass
            })
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    handleClick(tab, event) {
      console.log(tab, event);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.login {
  padding: 50px;
  margin: 0 auto;
  .el-tabs {
    width: 500px;
    margin: 0 auto;
  }
}
</style>
