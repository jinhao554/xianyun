<template>
    <div style="padding:25px">
        
        <el-form
        :model="form"
        :rules="rules"
        ref="form" 
        >
            <!-- 用户名的输入框 -->
            <el-form-item prop="username">
                <el-input 
                placeholder="用户名/手机" 
                v-model="form.username">
                </el-input>
            </el-form-item>

            <!-- 密码的输入框 -->
            <el-form-item prop="password">
                <el-input 
                placeholder="密码" 
                type="password" 
                v-model="form.password">
                </el-input>
            </el-form-item>

            <el-button 
            type="primary" 
            style="width:100%;"
            @click="handleSubmit"
            >登录</el-button>
        </el-form>
    </div>
</template>

<script>
export default {
    data(){
        return {
            form: {
                username: "",
                password: ""
            },

            rules: {
                username: [
                    { required: true, message: "请输入用户名", trigger: "blur" }
                ],
                password: [
                    { required: true, message: "请输入密码", trigger: "blur" }
                ]
            }
        }
    },

    methods: {
        // 提交登录事件
        handleSubmit(){

            this.$refs.form.validate(valid => {
                
                if(valid){
                    this.$store.dispatch("user/login", this.form).then(res => {
                        this.$message.success("登录成功");
                        setTimeout(() => {
                           this.$router.push("/") 
                        }, 1000);
                        
                    });
                }
            })

        }
    }
}
</script>

<style>

</style>
