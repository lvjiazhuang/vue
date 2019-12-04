<template>
	<div class="index-wrap">
		<div class="index-left">
			<div class="index-left-block">
				<h2>全部产品</h2>
				<template v-for="product in productList">
					<h3>{{ product.title }}</h3>
					<ul>
						<li v-for="item in product.list">
							<a :href="item.url">{{ item.name }}</a>
							<span class="hot-tag" v-if="item.hot">HOT</span>
						</li>
					</ul>
					<div class="hr" v-if="!product.last"></div>
				</template>
			</div>
			<div class="index-left-block lastest-news">
				<h2>最新消息</h2>
				<ul>
					<li v-for="item in newsList">
						<a :href="item.url">{{ item.title }}</a>
					</li>
				</ul>
			</div>
		</div>
		<div class="index-right">
			<slide-show :slides="slides" :inv="invTime" @onchange="doChangeSlide"></slide-show>
			<div class="index-board-list">
				<div class="index-board-item"
					 v-for="(item,index) in boardList" :class="['index-board-' + item.id,{'line-last':(index + 1) % 2 === 0}]">
					 <div class="index-board-item-inner">
					 	<h2>{{ item.title }}</h2>
					 	<p>{{ item.description }}</p>
					 	<div class="index-board-button">
					 		<router-link class="button" :to="{path: 'detail'}">立即购买</router-link>
					 	</div>
					 </div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import slideShow from '../components/slideShow'
	export default {
		name: 'index',
		components: {
			slideShow
		},
		created: function(){
			/*this.$http.get('/api/appData')
			.then(function(data){
				console.log(data)
			},function(err){
				console.log(err)
			})*/
		},
		methods: {
			doChangeSlide(props){
				//console.log('this is image index -> ' + props)
			}
		},
		data() {
			return {
				invTime:　3000,
				slides: [
					{
						src: require('../assets/slideShow/pic1.jpg'),
						title: '开发产品',
						href: 'detail/count'
					},
					{
						src: require('../assets/slideShow/pic2.jpg'),
						title: '品牌营销',
						href: 'detail/forecast'
					},
					{
						src: require('../assets/slideShow/pic3.jpg'),
						title: '使命必达',
						href: 'detail/analysis'
					},
					{
						src: require('../assets/slideShow/pic4.jpg'),
						title: '勇攀高峰',
						href: 'detail/publish'
					}
				],
				productList: {
					pc: {
						title: 'PC产品',
						list: [
							{
								name: '数据统计',
								url: 'http://www.baidu.com'
							},
							{
								name: '数据预测',
								url: 'http://www.baidu.com'
							},
							{
								name: '流量分析',
								url: 'http://www.baidu.com',
								hot:　true
							},
							{
								name: '广告发布',
								url: 'http://www.baidu.com'
							}
						]
					},
					app: {
						title: '手机应用类',
						last: true,
						list: [
							{
								name: '91助手',
								url: 'http://www.baidu.com'
							},
							{
								name: '产品助手',
								url: 'http://www.baidu.com',
								hot: true
							},
							{
								name: '智能地图',
								url: 'http://www.baidu.com'
							},
							{
								name: '团队语音',
								url: 'http://www.baidu.com'
							}
						]
					}
				},
				newsList: [
					{
						title: '新闻条目1',
						url: 'http://www.baidu.com'
					},
					{
						title: '新闻条目2',
						url: 'http://www.baidu.com'
					},
					{
						title: '新闻条目3',
						url: 'http://www.baidu.com'
					},
					{
						title: '新闻条目4',
						url: 'http://www.baidu.com'
					}
				],
				boardList: [
					{
						title: '开发产品',
						description: '开发产品是一款开放产品',
						id: 'car',
						saleout: false
					},
					{
						title: '品牌营销',
						description: '品牌营销帮助你的产品找到更好的定位',
						id: 'loud',
						saleout: false
					},
					{
						title: '使命必达',
						description: '使命必达快速迭代永远保持最前端的速度',
						id: 'earth',
						saleout: true
					},
					{
						title: '勇攀高峰',
						description: '帮你勇闯高峰，到达事业的登峰',
						id: 'hill',
						saleout: false
					}
				]
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	@import '../../css/base.css';
	*{
		margin:0;
		padding:0;
	}
	ul,li,p,ol,h1,h2,h3,h4,h5,h6,form,label,dl,dt,dd,header,footer,nav,section,aside,dialog,figure,figcaption,hgroup,article{
		display:block;
	}
	body{
		background-color: #f0f2f5;
		font-size: 14px;
		color: #444;
		margin: 0;
	}
	ul{
		list-style:none;
	}
	a,u{
		text-decoration:none;
	}
	table {
		border-collapse:collapse;
		border-spacing:0;
	}
	.index-wrap{
		width: 1200px;
		margin: 0 auto;
		overflow: hidden;
	}
	.index-left{
		float: left;
		width: 300px;
	}
	.index-right{
		width: 900px;
		float: left;
	}
	.hr{
		margin-bottom: 10px;
		height: 1px;
		background-color: #ccc;
	}
	.index-left-block{
		margin: 15px;
		background-color: #fff;
		box-shadow: 0 0 1px #ddd;
	}
	.index-left-block h2{
		text-align: center;
		padding: 10px 15px;
		margin-bottom: 20px;
		background-color: #4fc08d;
		font-size: 20px;
		color: #fff;
	}
	.index-left-block h3{
		padding: 0 15px 5px 15px;
		font-weight: bold;
		color: #222;
	}
	.index-left-block ul{
		padding: 10px 15px;
	}
	.index-left-block li{
		padding: 5px;
	}
	.index-left-block li a{
		color: #333;
	}
	.index-board-list{
		overflow: hidden;
	}
	.index-board-item{
		float: left;
		width: 400px;
		background-color: #fff;
		box-shadow: 0 0 1px #ddd;
		padding: 20px;
		margin-right: 20px;
		margin-bottom: 20px;
	}
	.index-board-item-inner{
		min-height: 125px;
		padding-left: 120px;
	}
	.index-board-car .index-board-item-inner{
		background: url(../assets/images/1.png) no-repeat;
	}
	.index-board-loud .index-board-item-inner{
		background: url(../assets/images/2.png) no-repeat;
	}
	.index-board-earth .index-board-item-inner{
		background: url(../assets/images/3.png) no-repeat;
	}
	.index-board-hill .index-board-item-inner{
		background: url(../assets/images/4.png) no-repeat;
	}
	.index-board-item h2{
		font-size: 18px;
		font-weight: bold;
		color: #000;
		margin-bottom: 15px;
	}
	.line-last{
		margin-right: 0;
	}
	.hot-tag{
		background-color: red;
		color: white;
	}
</style>
