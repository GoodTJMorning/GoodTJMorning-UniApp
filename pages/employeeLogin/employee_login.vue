<template>
	<view class='employee-login'>
		<uni-nav-bar
		  @clickLeft="goBack"
		  left-icon="back"
		  leftIcon="arrowleft"
		  title="楼长登录"
		  statusBar="true"
		  fixed="true"
		  color="#000000"
		  backgroundColor="#a7f3c9"
		></uni-nav-bar>
		<view class="container">
			<img src="@/image/img/logo-new.png" class="logo"/>

			<form >
				<view class="form-group">
					<lable for="username">账号: </lable>
					<input type="text" id="username" v-model="username" required>
				</view>
				<view class="form-group">
					<label for="password">密码</label>
					<input type="password" id="password" v-model="password" required>
				</view>
				<button type="submit" @click="login()" class="btn btn-primary small-button">登录</button>
			</form>
			<hr/>
			<view v-if="error" class="error">{{ error }}</view>

			<view class="contact-section">
				<h2>联系管理员，加入楼长队伍！</h2>
				<button @click="showImage">我要赚钱</button>
			</view>
		</view>
		
	</view>
</template>

<script>
import { mapState } from "vuex";
import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
import { employeeLogin } from "../api/api";
	export default {
		components: {
		  uniNavBar,
		  // Empty,
		},
		name: 'EmployeeLogin',
		data() {
			return {
				username: '',
				password: '',
				error: ''
			}
		},
		computed: {
			...mapState(["addressBackUrl"]),
		},
		methods: {
			goBack() {
				uni.redirectTo({
					url: this.addressBackUrl,
				});
			},
			login() {
				const params = {
					username : this.username,
					password : this.password
				}
				employeeLogin(params).then((res) => {
					if (res.code === 1) {
						console.log("success");
						uni.navigateTo({
							url:'/pages/employeeOrder/employeeOrder'
						});
					}
					else {
						this.error = '无效的用户名和密码'
					}
				})
			},
			showImage() {
			    uni.navigateTo({
			        url: '/pages/employeeOrder/employeeOrder'
					//'/pages/employee/employee_QRcode'
			    });
			}
		}
	}
</script>

<style lang="scss" scoped>
.employee-login {
  background-color: #f1fef7;
  height: 100vh;
  display: block;
  align-items: center;
  justify-content: center;

  .container {
    background: #f1fef7;
    padding: 20px;
    width: 90%;
	height:81%;
    max-width: 400px;
    border-radius: 10px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
	
	.logo {
	  width: 100%;
	  height: 100px;
	  margin: 0 auto 20px;
	}
	.small-button {
	  padding: 5px;
	  font-size: 1.2em;
	}

	hr {
	  border: none;
	  border-top: 1px solid #ddd;
	  margin: 20px 0;
	}

	.contact-section {
	  text-align: center;

	  h2 {
		margin-bottom: 15px;
	  }

	  button {
		padding: 10px;
		font-size: 1.1em;
		color: black;
		border: none;
		border-radius: 5px;
		cursor: pointer;
		background-color: #a7f3c9;
	  }

	}
  
    form {
      display: flex;
      flex-direction: column;

      .form-group {
        display: flex;
        flex-direction: column;
        margin-bottom: 15px;
      }

      input {
        padding: 10px;
        border-radius: 5px;
        border: 1px solid #ddd;
      }

      button {
        padding: 10px;
        background-color: #148F77;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;

        &:hover {
          background-color: #45B39D;
        }
      }
    }

    .error {
      color: red;
      margin-top: 10px;
    }
  }
}
</style>