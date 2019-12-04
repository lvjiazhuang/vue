<template>
	<div class="slide-show" @mouseover="clearInv" @mouseout="renInv">
		<div class="slide-img">
			<a :href="slides[nowIndex].href">
				<transition name="slide-trans">
					<img v-if="isShow" :src="slides[nowIndex].src" />
				</transition>
				
				<transition name="slide-trans-old">
					<img v-if="!isShow" :src="slides[nowIndex].src" />
				</transition>
			</a>
		</div>
		<h2>{{ slides[nowIndex].title }}</h2>
		<ul class="slide-pages">
			<li @click="goto(prevIndex)">&lt;</li>
			<li v-for="(item,index) in slides" @click="goto(index)">
				<a :class="{on: index === nowIndex}">{{ index+1 }}</a>
			</li>
			
			<li @click="goto(nextIndex)">&gt;</li>
		</ul>
	</div>
</template>
<script>
	export default {
		name: 'slideShow',
		props: {
			slides: {
				type: Array,
				default: []
			},
			inv: {
				type: Number,
				default: 3500
			}
		},
		data() {
			return {
				nowIndex: 0,
				isShow: true
			}
		},
		computed: {
			prevIndex(){
				if(this.nowIndex === 0){
					return this.slides.length - 1;
				}else{
					return this.nowIndex -1;
				}
			},
			nextIndex(){
				if(this.nowIndex === this.slides.length-1){
					return 0;
				}else{
					return this.nowIndex +1;
				}
			}
		},
		methods: {
			goto(index){
				this.isShow = false;
				setTimeout(() => {
					this.isShow = true;
					this.nowIndex = index;
					this.$emit('onchange',index);
				},10);
			},
			renInv(){
				this.invId = setInterval(() => {
					this.goto(this.nextIndex)
				},this.inv)
			},
			clearInv(){
				clearInterval(this.invId)
			}
		},
		mounted(){
			this.renInv();
			console.log(this.slides);
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.slide-trans-enter-active{
		transition: all .5s;
	}
	.slide-trans-enter{
		transform: translateX(900px);
	}
	.slide-trans-old-leave-active{
		transition: all .5s;
		transform: translateX(-900px);
	}
	.slide-show{
		position: relative;
		margin: 15px 15px 15px 0;
		width: 900px;
		height: 350px;
		overflow: hidden;
	}
	.slide-show h2{
		position: absolute;
		width: 100%;
		height: 30px;
		background-color: #000;
		color: #fff;
		opacity: .5;
		bottom: 0;
		text-align: left;
		padding-left: 15px;
	}
	.slide-img{
		width: 100%;
	}
	.slide-show img{
		width: 100%;
		position: absolute;
		top: 0;
	}
	.slide-pages{
		position: absolute;
		bottom: 0;
		right: 15px;
		z-index: 4;
	}
	.slide-pages li{
		height: 30px;
		line-height: 30px;
		float: left;
		font-size: 16px;
		color: #fff;
		margin: 0 20px;
		padding: 0 10px;
		cursor: pointer;
	}
	.on{
		color: #4fc08d;
		font-weight: bold;
	}
</style>