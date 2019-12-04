<template>
	<div>
		<div class="app-head bg-main">
			<div class="app-head-inner flex flex-row flex-h-between">
        <router-link :to="{path : '/'}">
          <img src="../assets/logo.gif" />
        </router-link>

				<div class="head-nav">
					<ul class="nav-list flex flex-row flex-h-between">
						<li @click="logClick">{{ username }}</li>
						<li class="nav-pile" v-if="username !== ''">|</li>
						<li @click="quit" v-if="username !== ''">退出</li>

						<li @click="logClick" v-if="username === ''">登陆</li>
						<li class="nav-pile" v-if="username === ''">|</li>
						<li @click="regClick" v-if="username === ''">注册</li>

						<li class="nav-pile">|</li>
						<li @click="aboutClick">关于</li>
					</ul>
				</div>
			</div>
		</div>

		<div class="app-content">
			<keep-alive>
				<router-view></router-view>
			</keep-alive>
		</div>

		<div class="app-foot">
			<p class="text-center">2017 author strong <i>人生苦短、我用JavaScript</i></p>
		</div>

		<my-dialog :is-show="isShowAboutDialog" @on-close="closeDialog('isShowAboutDialog')">
			<p>
				吕佳壮<br />
				移动互联网坚定不移的追随者<br />
				熟悉HTML5和CSS3布局网页、并了解兼容性<br />
				喜欢原生JavaScript<br />
				可以使用MUI框架开发webApp<br />
				了解ECMAScript6基本语法<br />
				熟悉使用Vue中指令，组件，路由，插槽，动画等构建项目<br />
				可以脱离库 开发
			</p>
		</my-dialog>

		<my-dialog :is-show="isShowLogDialog" @on-close="closeDialog('isShowLogDialog')">
			<log-form @has-log="onSuccessLog"></log-form>
		</my-dialog>

		<my-dialog :is-show="isShowRegDialog" @on-close="closeDialog('isShowRegDialog')">
			<p> reg Vue</p>
			<reg-form></reg-form>
		</my-dialog>
	</div>
</template>

<script>
	import Dialog from './dialog';
	import LogForm from './logForm';
	import RegForm from './regForm';
	export default {
		name: 'layout',
		components: {
			MyDialog: Dialog,
			LogForm,
			RegForm
		},
		data() {
			return {
				isShowAboutDialog: false,
				isShowLogDialog: false,
				isShowRegDialog: false,
				username: ''
			}
		},
		methods: {
			aboutClick(){
				this.isShowAboutDialog = true;
			},
			logClick(){
				this.isShowLogDialog = true;
			},
			regClick(){
				this.isShowRegDialog = true;
			},
			closeDialog(myAttr){
				this[myAttr] = false;
			},
			onSuccessLog(data){
				this.closeDialog('isShowLogDialog');
				this.username = data.username;
			},
			quit(){
        this.username = '登陆'
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
	@import '../../css/base.css';
	.app-head{
		height: 90px;
		line-height: 90px;
		color: #b2b2b2;
	}
	.app-head-inner{
		width: 1200px;
		margin: 0 auto;
	}
	.app-head-inner img{
		width: 114px;
		padding: 7px 0;
	}
	.head-nav li{
		cursor: pointer;
	}
	.head-nav .nav-pile{
		padding: 0 10px;
		cursor: inherit;
	}


	.app-content{
		width: 1200px;
		margin: 0 auto;
	}


	.app-foot{
		height: 80px;
		line-height: 80px;
		background-color: #e3e4e8;
	}

	.index-board-button{
		margin-top: 15px !important;
	}
	.button {
		display: block;
		width: 100px;
		height: 35px;
		line-height: 35px;
		background-color: #4fc08d;
		text-align: center;
		color: #fff;
		cursor: pointer;
	}
	.g-form-line{
		padding: 15px;
	}
	.g-form-label{
		width: 100px;
		font-size: 16px;
		color: #666;
		display: inline-block;
	}
	.g-form-input{
		display: inline-block;
	}
	.g-form-input input{
		width: 200px;
		height: 30px;
		line-height: 30px;
		vertical-align: middle;
		padding: 0 10px;
		border: 1px solid #ccc;
	}
	.g-form-error{
		color: red;
		padding-left: 15px;
	}
	/*.g-form-btn{
		padding-top: 100px;
	}*/
</style>
