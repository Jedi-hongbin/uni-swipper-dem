<template>
	<view class='container' :style="{'background-color':bgc,'height': loadHeight || '100vh'}">
		<text>{{title}}</text>
		<text>height: {{loadHeight}}</text>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				loadHeight: ''
			}
		},
		props:{
			index: Number,
			title: String,
			height: String,
			bgc: String,
			currentSwipperIndex: Number
		},
		created() {
			if (this.currentSwipperIndex === this.index) {
				this.request();
			} 
		},
		methods:{
			async request(){
				uni.showLoading({
					title:"loading..."
				});
				//模拟请求操作
				await new Promise((resolve, reject) => {
					setTimeout(() => {
						this.loadHeight = this.height;
						setTimeout(() => {
							
						this.$emit("onLoadComplete");
						},0)
						uni.hideLoading();
					},1000)
				});
			}
		},
		watch:{
			currentSwipperIndex:{
					handler(newVal){
						if (newVal === this.index) { this.request();}
					}
			}
		}
	}
</script>

<style>
	.container{
		background-color: #00FFFF;
		height: 100vh;
	}
</style>
