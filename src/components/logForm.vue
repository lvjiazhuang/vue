<template>
	<div class="login-form">
		<div class="g-form">
			<div class="g-form-line">
				<span class="g-form-label">用户名：</span>
				<div class="g-form-input">
					<input type="text" placeholder="请输入用户名" v-model="userNameModel" />
				</div>
				<span class="g-form-error">{{ userError.errorText }}</span>
			</div>

			<div class="g-form-line">
				<span class="g-form-label">密码：</span>
				<div class="g-form-input">
					<input type="password" placeholder="请输入密码" v-model="passwordModel" />
				</div>
				<span class="g-form-error">{{ passwordErrors.errorText }}</span>
			</div>

			<div class="g-form-line">
				<div class="g-form-btn">
					<a class="button" @click="onLogin">登陆</a>
				</div>
			</div>
			<p>{{ errorOut }}</p>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				userNameModel: '',
				passwordModel: '',
				errorOut: ''
			}
		},
		computed: {
			userError(){
				let errorText, status;
				if(!/@/g.test(this.userNameModel)){
					status = false;
					errorText = '输入中不包含 @ ';
				}else{
					status = true;
					errorText = '';
				}
				if(!this.userFlag){
					errorText = '';
					this.userFlag = true;
				}
				return{
					status,
					errorText
				}
			},
			passwordErrors(){
				let errorText, status;
				if(!/^\w{1,6}$/g.test(this.passwordModel)){
					status = false;
					errorText = '密码请输入1-6位'
				}else{
					status = true;
					errorText = '';
				}
				if(!this.passwordFlag){
					errorText = '';
					this.passwordFlag = true;
				}
				return{
					status,
					errorText
				}
			}
		},
		methods: {
			onLogin(){
				if(this.userError.status || this.passwordErrors.status){
					this.errorOut = '';
					/* this.$http.get('http://localhost:8081/login')
					.then((res) => {
						this.$emit('has-log',res.data);
					},(error) => {
						console.log(error);
					}) */
          this.$emit('has-log',{username: this.userNameModel});
				}else{
					this.errorOut = '部分信息输入错误，请更改'
				}
			}
		}
	}
</script>

<style scoped>

</style>
