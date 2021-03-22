<template>
	<view class="wrapper">
		
	<view class="btn_tab">
		<button :class="currentTab === 0 ? 'active' : undefined" @click="toggerTab(0)">1</button>
		<button :class="currentTab === 1 ? 'active' : undefined" @click="toggerTab(1)">2</button>
		<button :class="currentTab === 2 ? 'active' : undefined" @click="toggerTab(2)">3</button>
	</view>
	
	<swiper :style="{'height':swiperHeight+'px'}" class="swiper" :current="currentTab" duration="300"
		@change="swiperTab">
		<swiper-item>
			<view class="container">
				<listCard @onLoadComplete="setSwiperHeight" title="1" height="1000px" bgc="red" :currentSwipperIndex="currentTab" index='0' />
			</view>
		</swiper-item>
		<swiper-item>
			<view class="container">
				<listCard @onLoadComplete="setSwiperHeight" title='2' height="600px" bgc="blue" :currentSwipperIndex="currentTab" index = '1'/>
			</view>
		</swiper-item>
		<swiper-item>
			<view class="container">
				<listCard @onLoadComplete="setSwiperHeight" title="3" height="100px" bgc="green" :currentSwipperIndex="currentTab" index = '2'/>
			</view>
		</swiper-item>
	</swiper>
	</view>
</template>

<script>
	import listCard from './listCard.vue'
	export default {
		data() {
			return {
				currentTab: 0,
				swiperHeight: ''
			}
		},
		methods: {
			toggerTab(index){
				this.currentTab = index
			},
			swiperTab(e) {
				this.currentTab = e.target.current;
				// this.setSwiperHeight()
			},			
			setSwiperHeight() {
				let query = uni.createSelectorQuery().in(this);
				query.selectAll(".container").boundingClientRect();
				query.exec((res) => {
					this.swiperHeight = res[0][this.currentTab].height;
					console.log(`height: ${this.swiperHeight}`,res)
				})
			}
		},
		components: {
			listCard
		}
	}
</script>

<style>
	.wrapper{
		
	}
	.btn_tab{
		display: flex;
		height: 30px;
		
	}
	.btn_tab button{
		flex :1;
		 margin: 3px;
		 font-size: 10px;
		 box-shadow: 0 0 10px 3px #ccc;
	}
	.active {
		background-color: #000;
		color: #FFFFFF;
		font-weight: bold;
	}
	.swiper {
		height: 100vh;
		max-width: 100vw;
	}
</style>
