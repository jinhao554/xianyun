<template>
  <!-- 公共样式组件 -->
  <header class="header">
    <el-row type="flex" justify="space-between" class="main">
      <div class="logo">
        <nuxt-link to="/">
          <img src="http://157.122.54.189:9093/images/logo.jpg" alt>
        </nuxt-link>
      </div>

      <!-- 导航条 -->
      <el-row type="flex" class="navs">
        <nuxt-link to="/">首页</nuxt-link>
        <nuxt-link to="/post">旅游攻略</nuxt-link>
        <nuxt-link to="/hotel">酒店</nuxt-link>
        <nuxt-link to="/air">国内机票</nuxt-link>
      </el-row>
      <!-- 登陆注册 -->
      <div class="PictureFrame">
        <div v-if="true">
          <el-dropdown>
            <span class="el-dropdown-link">
              <img src="http://157.122.54.189:9095/assets/images/avatar.jpg" alt>
              🐖皮球
              <i class="el-icon-arrow-down el-icon--right"></i>
            </span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人中心</el-dropdown-item>
              <el-dropdown-item>退出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div> 

        <div class="login-link" v-else>登录 / 注册</div>
      </div>
    </el-row>
  </header>
</template>
<script>
export default {
};
</script>
<style lang="less" scoped>
.header {
  height: 60px;
  line-height: 60px;
  border-bottom: 1px #ddd solid;
  box-shadow: 0 2px 2px #eee;

  .main {
    width: 1000px;
    margin: 0 auto;

    .logo {
      margin-top: 9px;
      margin-right: 20px;

      img {
        display: block;
        width: 156px;
        height: 42px;
      }
    }

    .navs {
      flex: 1;

      a {
        display: block;
        padding: 0 20px;
        height: 60px;
        box-sizing: border-box;

        &:hover {
          color: #409eff;
          border-bottom: 5px #409eff solid;
        }

        &:active {
          background: #409eff;
          color: #fff;
        }
      }

      // 高亮的样式
      .nuxt-link-exact-active {
        background: #409eff;
        color: #fff !important;
      }
    }

    // 登录 注册的样式
    .PictureFrame {
      img {
        width: 36px;
        height: 36px;
        border-radius: 100px;
        vertical-align: middle;
      }
    }
  }
}
</style>
