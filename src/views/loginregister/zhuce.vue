<template>
	<div class="wrapper">
		<div class="img">
			<img src="../../image/login1.png"/>
		</div>
		<div class="login">
			<p><router-link to="/login">登陆</router-link></p>
			<p><router-link to="/zhuce">注册</router-link></p>
		</div>
		<div class="container">
			<div class="left" v-show="isLogin">
				
					<InputComponent
						placeholder="请输入手机号"
						
						
					/>
				<!--v-on:change="registergetMyPhone"-->
				<!--<div class="tel">
					<img src="../../image/login2.png"/>
					<input type="text" name="" placeholder="请输入手机号" />
					
				</div>-->
				<!--<div class="tel">
					<img src="../../image/login3.png"/>
					<input type="text" name="" placeholder="请输入验证码" />
				</div>-->
						<InputComponent
						placeholder="请输入验证码"
						v-on:change="getPassword"
						
					/>
				<!--<div class="tel">
					<img src="../../image/login2.png"/>
					<input type="text" name="" placeholder="请输入密码" />
					
				</div>-->
						<InputComponent
						placeholder="请输入密码"
						v-on:change="getPassword"
						
					/>
				<!--<div class="tel">
					<img src="../../image/login3.png"/>
					<input type="text" name="" placeholder="请再次输入密码" />
				</div>-->
						<InputComponent
						placeholder="请再次输入密码"
						v-on:change="getPassword"
						
					/>
				<div>
					<button @click="loginEvent">注册</button>
				</div>
				
			</div>
			<div class="right" v-show="!isLogin"></div>
		</div>
	</div>
	
</template>


<script>
	import axios from 'axios'
import { getList } from '../../service/AppService'
	
import InputComponent from "../../components/inputComponent"
import Button from "../../components/Button"
	
	export default{
		data:function(){
			return{
				isLogin:true,
				userName:'',
				passWord:'',
				isShowPhone:false,
				isShowPsd:false
			}
		},
		components:{InputComponent,Button},
		created: function () {
	      getList().then(function (value) {
	        console.log(value)
	      });
	    },
//	    定义事件
		methods:{
			getMyPhone: function (data) {
		        
		        this.userName=data
		      },
		      getPassword:function(data){
		      	this.passWord=data
		      },
////		      显示注册
		      loginChoiceEvent:function(){
		      	this.isLogin=true
		      },
		      registerChoiceEvent:function(){
		      	this.isLogin=false
		      },
		      phoneBlurEvent:function(data){
		      	console.log('userName',data);
		      	if(data){
		      		this.isShowPhone=false
		      	}
		      	else{
		      		this.isShowPhone=true
		      	}
		      },
		      psdBlurEvent:function(data){
		      	console.log('userName',data);
		      	if(data){
		      		this.isShowPhone=false
		      	}
		      	else{
		      		this.isShowPhone=true
		      	}
		      },
		      loginEvent:function () {
		        var userName = this.userName;
		        var passWord = this.passWord;
		        console.log(userName,)
		       if(userName && passWord,passWord){
			       axios.post('http://114.55.249.153:8028/login/LoginByPhone', {
			          phone: userName,
			          password: passWord
			        })
			          .then(function (response) {
			            console.log('login',response);
			            this.$router.replace('/')
			          }.bind(this))
			          .catch(function (error) {
			            console.log(error);
			          });
			      }
			      
		      
			      else{
			      	this.userName && (this.isShowPhone=false);
			      	!this.userName && (this.isShowPhone=true);
			      	this.passWord && (this.isShowPsd=false);
			      	!this.passWord && (this.isShowPsd=true);
			      }
				}
		     }
	}
</script>

<style type="text/css" lang="scss" scoped="" >
	/*@import './css/commin'*/
	.center{
		text-align: center;
	}
	.wrapper{
		margin: 0;
		padding: 0;
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		
	}
	.img{
		margin-top: -20px;
		height: 180px;
		width: 100%;
	}
	.img img{
		height: 180px;
		width: 100%;
	}
	.login{
		width: 100%;
		height: 60px;
		/*line-height: 60px;*/
		display: flex;
		background: gainsboro;
		flex-direction: row;
		text-align: center;
		margin-top: -20px;
	}
	.login p{
		flex: 1;
	}
	.login p a{
		text-decoration: none;
	}
	.container{
		width: 100%;
		
		flex: 1;
		
	}
	.container .left div{
		margin-top: 24px;
		
	}
	.container .left button{
		width: 92%;
		height: 50px;
		border: none;
		border-radius: 17px;
		margin: 0px auto;
		background: #B92C28;
		color: white;
		/*margin: 0 20px;*/
		margin-left: 20px;
		font-size: 20px;
	}
	.container .left .tel{
		width: 90%;
		margin: 0 auto;
		
		height: 60px;
		border-bottom: 2px solid gainsboro;
	}
	.container .left .tel input{
		border: none;
		padding-top: 20px;
		text-indent: 4rem;
	}
</style>