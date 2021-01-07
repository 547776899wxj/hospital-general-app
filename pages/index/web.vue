<template>
	<view >
		<!-- <view class="uni-form-item form-item-bottom" :style="zIndex">
			<button class="popup-btn" @click="navTo">路径错误点击返回</button>
		</view> -->
		<!-- <web-view class="content" src="https://www.baidu.com/?tn=48021271_22_hao_pg" @message="handleMessage" ></web-view> -->
		<web-view :src="url" @message="handleMessage" ></web-view>
	</view>
</template>

<script>
	// #ifdef APP-PLUS
		var FvvUniTTS = uni.requireNativePlugin('Fvv-UniTTS');
	// #endif
	export default {
		data() {
			return {
				url:'',
				zIndex:{
					'z-index':1000
				},
			}
		},
		onLoad() {
			// #ifdef H5
				this.zIndex = {'z-index':0};
			// #endif
			this.url = uni.getStorageSync('ip')+'/#/pages/'+uni.getStorageSync('path');
		},
		methods: {
			navTo(){
				console.log(123);
				uni.navigateTo({
					url: 'index?webView=true',
				});
			},
			handleMessage(res) {
				// 获取网页的参数
				let data = res.detail.data[0];
				if(data.status){
					this.zIndex = 0;
				}
				if(data.reload){
					// #ifdef APP-PLUS
					var currentWebview = this.$mp.page.$getAppWebview() //获取当前页面的webview对象
					var wv = currentWebview.children()[0]
					wv.reload();
					// #endif
					return
				}
				console.log(data.text);
				// #ifdef APP-PLUS
					if(data.text){
						FvvUniTTS.init((callback) => {
							FvvUniTTS.speak({
								text:data.text
							});
						});
					}
				// #endif
			},
		}
	}
</script>

<style>
	page{
		height: 100%;
	}
	.content{
		height: 1920px;
	}
	.uni-form-item {
		display: flex;
		align-items: center;
		padding: 40rpx 40rpx 0 40rpx;
		justify-content: center;
		position: fixed;
		top: 0;
		
	}
	.popup-btn {
		font-size: 20rpx;
		color: #fff;
		padding-left: 40rpx;
		padding-right: 40rpx;
		background-color: rgb(68, 114, 196);
		margin-left: 40rpx;
		margin-right: 40rpx;
	}
</style>
