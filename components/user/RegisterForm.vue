<template>
    <el-form 
        :model="form" 
        ref="form" 
        :rules="rules" 
        class="form">
            <el-form-item class="form-item" prop="username">
                <el-input 
                placeholder="请输入手机号码"
                v-model="form.username"
                >
                </el-input>
            </el-form-item>

            <el-form-item class="form-item" prop="captcha">
                <el-input 
                placeholder="输入验证码"
                v-model="form.captcha"
                 >
                    <template slot="append">
                        <el-button @click="handleSendCaptcha">
                            发送验证码
                        </el-button>
                    </template>
                </el-input>
            </el-form-item>

            <el-form-item class="form-item" prop="nickname">
                <el-input 
                placeholder="输入你的大名"
                v-model="form.nickname"
                >
                </el-input>
            </el-form-item>

            <el-form-item class="form-item" prop="password">
                <el-input 
                placeholder="密码" 
                type="password"
                v-model="form.password"
                ></el-input>
            </el-form-item>

            <el-form-item class="form-item" prop="checkPassword">
                <el-input 
                placeholder="再次确认密码" 
                type="password"
                v-model="form.checkPassword"
                >
                </el-input>
            </el-form-item>

            <el-button 
            class="submit" 
            type="primary" 
            @click="handleRegSubmit">
                注册
            </el-button>
        </el-form>
</template>

<script>
export default {
    data(){
         //确认密码
          const validatePass = (rule,value,callback)=>{
                  if( value ===''){
                      callback(new Error('请再次输入密码'))
                  }else if(value !==this.form.password){
                      callback(new Error('两次输入密码不一致'))
                  }else{
                      callback();
                  }
            }
          return {
            // 表单数据
            form: {
                username:'',//用户名
                password:'',//密码
                checkPassword:'',//确认密码
                nickname:'',//名字
                captcha:'',//验证码
            },
            // 表单规则
            rules: {
                 username:[
                        {required: true,message: '请输入手机号码',trigger: 'blur'}
                     ],
                 password:[
                        {required: true,message: '请输入密码',trigger: 'blur'}
                     ],
                 checkPassword:[
                        { validator: validatePass, trigger: 'blur'}
                     ],
                 nickname:[
                        { required: true, message: '请输入昵称', trigger: 'blur'}
                ],
                 captcha:[
                    { required: true, message: '请输入验证码', trigger: 'blur'}
                ],
            },
        }  
    },
    methods: {
        // 获取验证码
        handleSendCaptcha(){
            //判断手机号码是否有11位数
           if(this.form.username.length !==11){
               this.$confirm('手机号码不对','知道没',{
                   confirmButtonText:'这里',
                   showCancelButton:false,
                   type:'warning'
               })
               return
           }
           this.$axios({
            //    发起请求获取验证码
               url:'/captchas',
               method:'POST',
               data:{
                   tel:this.form.username
               }
           }).then(reslut=>{
            //    console.log(reslut)
            const { code }=reslut.data
            // console.log(code)
               this.$confirm(`验证码:${code}`,'知道没',{
                   confirmButtonText:'这里',
                   showCancelButton:false,
                   type:'warning'
               })

           })
        },  // 注册
        handleRegSubmit(){
          this.$refs.form.validate((valid)=>{
              if(valid){
                  const {checkPassword,...props}=this.form
                  this.$axios({
                      url:'/accounts/register',
                      method:'POST',
                      data:props
                  }).then(reslut=>{
                      console.log(reslut.data)
                  })
              }
          })
        }
    }
}
</script>

<style scoped lang="less">
    .form{
        padding:25px;
    }

    .form-item{
        margin-bottom:20px;
    }

    .form-text{
        font-size:12px;
        color:#409EFF;
        text-align: right;
        line-height: 1;
    }

    .submit{
        width:100%;
        margin-top:10px;
    }
</style>