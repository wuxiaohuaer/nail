<template>
    <header class="head">
        <img class="h1" src="../../../assets/imgs/h1.png" alt="">
        <div class="float-right" ref="title">
            <nav class="nav">
                <!-- <div class="lis">{{$t("home")}}</div> -->
                <!-- <div class="lis">{{$t("Assets")}}</div>
                <div class="lis">{{$t("Introduction")}}</div> -->
            </nav>
            <div class="lis-login">
                <div @click="login" class="btnlogin">{{$t("Login")}}/</div>
                <div @click="register" class="btnregister">{{$t("Register")}}</div>
            </div>
            <!-- <select class="lange" @change="handchange($event)" ref="aaa">
                <option class="desfont" v-for="(index,value) in langu" :value="value" :key="value">{{index}}</option>
                <img src="../../../assets/imgs/xiala.png" alt="">
            </select> -->
            <BaseSelect v-on:select="showProject"
              :selectedValue="projectName"
              :dataList="list"
              :widthData="widthData"></BaseSelect>
        </div>
    </header>
</template>

<script>
import BaseSelect from '../../../components/xiala'
import { mapState,mapMutations } from 'vuex'
import axios from 'axios'
export default{
    name:'IndexHeader',
    components:{
        BaseSelect
    },
     data(){
      return {
          list:[
          {key:"zh",value:"中文"},
          {key:"en",value:"English"},
          {key:"ja",value:"日本語"}
        ],
        projectName:{//岁子组件的选择值改变而改变的值
          key:"",
          value:""
        },
        widthData:"60px",
      }
    },
    // updated() {
    //     let lang = window.localStorage.getItem('language')
    // },
    // mounted(){
    //     let lan = window.localStorage.getItem('language')
    //     if (lan) {
    //         this.$refs.aaa.value = lan
    //     }
    // },
    methods:{
      handchange(event){
        this.$i18n.locale = event.target.value
        window.localStorage.setItem('language', event.target.value)
        window.localStorage.setItem('lang', this.langu[event.target.value])
      },
      showProject (){
            var params = new URLSearchParams();
            let token = localStorage.token
            params.append('language', this.projectName.key);
            params.append('token', token);
            let that = this;
            axios({
			url:' http://www.nailfuture.com/Userapi/currencyList',
			method: 'post',
			data: params,
            })
            .then(function (res) {
                if (res.data.msg == 'success') {
                     that.$store.commit('getlist',res.data.data)
                }
            })
            .catch(function (error) {
                console.log(error);
            });
      },
      login(){
          let register = document.querySelector('.register-wrap')
          let login = document.querySelector('.login-wrap')
          register.style.display = 'none'
          login.style.display = 'block'
      },
      register(){
          let register = document.querySelector('.register-wrap')
          let login = document.querySelector('.login-wrap')
          register.style.display = 'block'
          login.style.display = 'none'
      }
    },
}
</script>
<style lang="less">
    .head{
        width: 100%;
        height: 128px;
        box-sizing: border-box;
        background: #3b3b3b;
        .h1{
            width: 136px;
            height: 38px;
            color: #757575;
            margin-left: 30px;
            position: relative;
            top: 35px;
            font: 48px/128px "华文细黑";
        }
        .float-right{
            float: right;
            margin-top: 28px;
            position: relative;
            
            font: 24px/63px "华文细黑";
            .nav{
                overflow: hidden;
                float: left;
                color: #757575;
                margin-right: 20px;
                .lis{
                    float: left;
                    text-align: center;
                    margin: 0  10px;
                }
                .lis:hover{
                    border-bottom: 1px solid #757575;
                }
            }
            .lis-login{
                overflow: hidden;
                position: relative;
                top: -7px;
                float: left;
                    color: #757575;
                    .btnlogin{
                        float: left;
                    }
                    .btnregister{
                        float: left;
                    }
            }
            .lange{
                background: transparent;
                float: right;
                margin-left: 10px;
                margin-right: 60px;
                color: #b9bcc3;
                text-align: center;
                font: 28px/68px "微软雅黑";
                -webkit-appearance: none; /*for chrome*/
                img{
                    width: 20px;
                    height: 10px;
                    // position: absolute;
                    // right: 40px;;
                    // top: 30px;
                }
            }
            
        }
    }
</style>

