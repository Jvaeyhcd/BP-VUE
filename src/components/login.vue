<template>
<div class="layout">
    <Layout>
        <Header>
            <Menu mode="horizontal" theme="light" active-name="1">
                <div class="layout-logo">
                  <img src="../assets/logo-top.png" alt="">
                </div>
                <div class="layout-nav">
                  <Button type="text">登录/注册</Button>
                </div>
            </Menu>
        </Header>
        <Content>
            <div class="bgimg">
              <div class="loginForm">
                <div class="title">手机验证码登录</div>
                <div class="in-icon" style="margin-top: 30px;margin-bottom: 10px;position: relative;">
                  <span><i class="headpic"></i></span>
                  <input class="bp-input" v-model="tel" placeholder="请输入手机号" maxlength="11" style="width: 300px" />
                </div>
                <div class="warn" v-if="telValidate">
                  <div style="float:left"><img src="../assets/warning.png" alt=""></div>
                  <span>手机号码错误</span>
                </div>
                <div class="in-icon" style="margin-top: 10px;margin-bottom: 10px;position: relative;overflow: hidden;">
                  <span><i class="pwdpic"></i></span>
                  <input class="bp-input" v-model="code" placeholder="请输入验证码" style="width: 180px;float: left;" />
                  <Button @click="getCode" style="float:left;margin-left:6px;width:112px;height: 40px;"><div style="color:#c63a47">{{getTxt}}</div></Button>
                </div>
                <div class="warn">
                  <div style="float:left"><img src="../assets/warning.png" alt=""></div>
                  <span>验证码错误</span>
                </div>
                <Button class="LoginBtn" @click="login">登录/注册</Button>
              </div>
            </div>
            <div class="footimg">
              <Header>
                <Menu mode="horizontal"  active-name="1">
                    <div style="height:30px;float:left;margin-left:20px;">
                      <img style="position: absolute;top: 5px;" src="../assets/logo-foot.png" alt="">
                    </div>
                    <ul class="foot-nav" style="position: absolute !important;list-style:none;">
                        <li name="1">
                            关于我们
                        </li>
                        <li name="2">
                            服务
                        </li>
                        <li name="3">
                            项目
                        </li>
                        <li name="4">
                            联系我们
                        </li>
                    </ul>
                </Menu>
            </Header>
            </div>
        </Content>
    </Layout>
    <Modal v-model="modal" width="360">
      <p slot="header" style="color:#f60;text-align:center">
        <Icon type="ios-information-circle"></Icon>
        <span>提示</span>
      </p>
      <div style="text-align:center">
        <p>该平台仅对创业者开发</p>
      </div>
      <div slot="footer">
        <Button type="error" size="large" long @click="confirm">确定</Button>
      </div>
    </Modal>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data:'',
      tel: "",
      password: "",
      getTxt: "获取验证码",
      telValidate:false,
      codeValidate:false,
      code:'',
      serverCode:'',
      isInvestor:false,
      isUserInfo:false,
      modal:false
    };
  },
  methods:{
    login(){
      this.$router.push({path: '/BPIndex'})
      // if(this.code != this.serverCode){
      //   this.codeValidate = true;
      // }else{
      //   this.codeValidate = false;
      //   this.$http.post('url',{  
      //     tel:this.tel,  
      //     code:this.code  
      //   },{  
      //     emulateJSON:true  
      //   }).then(function(response){  
      //     this.data = response.data;
      //     // this.isInvestor =
      //     // this.isUserInfo =
      //     if(!this.isInvestor){
      //       if(this.isUserInfo){
      //         this.$router.push({path: '/BPIndex'})
      //       }else{
      //         this.$router.push({path: '/userInfo'})
      //       }
      //     }else{
      //       this.modal = true;
      //     }
      //   },function(response){  
      //     console.log(response)
      //   });
      // }
    },
    getCode(){
      if(this.tel.substring(0,1) != '1' || this.tel.length != 11){
        this.telValidate = true;
      }else{
        this.telValidate = false;
        this.$http.get('url',{
          tel:this.tel
        }).then(function(response){
          this.serverCode = response.data.code;
        },function(response){  
          console.log(response)
        });
      }
    },
    confirm(){
      this.modal = false;
    }
  },
  mounted(){

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bp-input {
  height: 40px;
  background-color: rgb(90, 90, 90);
  border: 1px solid rgb(90, 90, 90);
  opacity: 0.6;
  border-radius: 5px;
  padding-left: 40px;
}
input::-webkit-input-placeholder {
  color: white;
}
input::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: white;
}
input:-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: white;
}
input:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: white;
}
.layout {
  border: 1px solid #d7dde4;
  background: #f5f7f9;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
}
.layout-logo {
  width: 100px;
  height: 40px;
  border-radius: 3px;
  float: left;
  position: relative;
  top: 15px;
  left: 20px;
}
.layout-nav {
  width: 85px;
  margin: 0 auto;
  margin-right: 20px;
}
.bgimg {
  background-image: url(../assets/bg.png);
  height: 890px;
  width: 100%;
}
.loginForm {
  height: 400px;
  width: 300px;
  position: absolute;
  top: 280px;
  left: calc(50% - 150px);
}
.title {
  color: white;
  text-align: left;
  font-size: 22px;
}
.headpic {
  display: inline-block;
  width: 40px;
  height: 40px;
  background-image: url(../assets/Male-User.png);
  background-position: center center;
  background-repeat: no-repeat;
  text-align: center;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
}
.pwdpic {
  display: inline-block;
  width: 40px;
  height: 40px;
  background-image: url(../assets/Lock-.png);
  background-position: center center;
  background-repeat: no-repeat;
  text-align: center;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
}
.in-icon span {
  width: 40px;
  height: 40px;
  text-align: center;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
}
.warn {
  height: 20px;
  line-height: 20px;
  text-align: left;
  color: white;
}
.warn span {
  opacity: 0.5;
  margin-left: 5px;
}
.LoginBtn{
  width:300px;
  margin-top: 30px;
  background-color:#c63a47;
  border: 1px solid #c63a47;
  color:white;
  font-size: 18px;
}
.footimg {
  background-image: url(../assets/footer.png);
  height: 30px;
  width: 100%;
  position: absolute;
  bottom: 0;
}
.footimg div,
.footimg div ul {
  background: transparent;
  height: 30px !important;
  position: unset !important;
}
.foot-nav {
  right: 70px;
}
.foot-nav li {
  float: left;
  width: 100px;
  color: white;
  height: 30px;
  line-height: 30px;
  cursor: pointer;
}
</style>
