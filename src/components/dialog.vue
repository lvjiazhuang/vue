<template>
	<div>
		<div class="dialog-wrap">
			<div class="dialog-cover" @click="closeMyself"  v-if="isShow"></div>
			<transition name="drop">
				<div class="dialog-content"  v-if="isShow">
					<p class="dialog-close" @click="closeMyself">X</p>
					<slot>empty</slot>
				</div>
			</transition>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			isShow: {
				type: Boolean,
				default: false
			}
		},
		data(){
			return {
				
			}
		},
		methods: {
			closeMyself(){
				this.$emit('on-close');
			}
		}
	}
		
</script>

<style scoped>
	.drop-enter-active{
		transition: all .5s ease;
	}
	.drop-leave-active{
		transition: all .3s ease;
	}
	.drop-enter{
		transform: translateY(-500px);
	}
	.drop-leave-active{
		transform: translateY(-500px);
	}
	
	.dialog-wrap{
		position: fixed;
		width: 100%;
		height: 100%;
	}
	.dialog-cover{
		width: 100%;
		height: 100%;
		background-color: #000;
		opacity: .3;
		position: fixed;
		z-index: 500;
		top: 0;
		left: 0;
	}
	.dialog-content{
		width: 50%;
		max-height: 50%;
		line-height: 1.6;
		overflow: hidden;
		background-color: #fff;
		position: fixed;
		top: 20%;
		left: 50%;
		margin-left: -25%;
		z-index: 1000;
		border: 2px solid #464048;
		padding: 3%;
	}
	.dialog-close{
		position: absolute;
		right: 15px;
		top: 10px;
		cursor: pointer;
		font-size: 20px;
		font-weight: bold;
	}
</style>