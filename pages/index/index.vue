<template>
	<view class="content">
		
		<view class="popup">
			<view class="popup-header">
				设置
			</view>
			<view>
				<form >
					<view class="uni-form-item " >
						<view class="popup-title" >ip：</view>
						<input class="uni-input" name="ip" v-model="ip" placeholder="如:(http://192.168.0.190:8081)" />
					</view>
					<view class="uni-form-item " >
						<view class="popup-title" >路径：</view>
						<input class="uni-input" name="path" v-model="path"  placeholder="如:(skin/skin)" />
					</view>
					<view class="uni-form-item " >
						<view class="popup-title" >高度：</view>
						<input class="uni-input" name="height"  v-model="height" placeholder="如:(1080)" />
					</view>
					<!-- <view class="uni-form-item " >
						<view class="popup-title" >刷新时间：</view>
						<input class="uni-input" name="height"  v-model="height" placeholder="如:()" />
					</view> -->
					<view class="uni-form-item ">
						<button class="popup-btn"   @click="clear" >清除</button>
						<button class="popup-btn"  @click="formSubmit" >确定</button>
					</view>
					<view class="uni-form-item form-item-bottom">
						<button class="popup-btn"  style="width: 100%;" @click="navTo()" >ip测试页</button>
					</view>
				</form>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ip:'',
				path:'',
				height:'1080',
				test:'',
				showWebView:false,
			}
		},
		onLoad(e) {
			this.ip = uni.getStorageSync('ip') || '';
			this.path = uni.getStorageSync('path') || '';
			this.height = uni.getStorageSync('height') || '';
			let webView = e.webView||false;
			if(this.ip && this.path && !webView){
				uni.navigateTo({
					url: 'webn',
				});
			}
		},
		methods: {
			//清除
			clear(){
				this.ip = '';
				this.path = '';
				this.height = '';
			},
			//确定
			formSubmit(e) {
				uni.setStorageSync('ip',this.ip);
				uni.setStorageSync('path',this.path);
				uni.setStorageSync('height',this.height);
				if(this.ip=='' || this.path==''){
					uni.showToast({
						title: 'ip或路径不能为空',
						icon:'none'
					});
					return
				}
				
				uni.redirectTo({
					url: 'webn',
				})
            },
			navTo(url){
				uni.setStorageSync('ip',this.ip);
				uni.setStorageSync('path',this.path);
				uni.setStorageSync('height',this.height);
				if(this.ip=='' || this.path==''){
					uni.showToast({
						title: 'ip或路径不能为空',
						icon:'none'
					});
					return
				}
				
				uni.navigateTo({
					url:'./test',
				})
			}
		}
	}
</script>

<style>
	.image{
		position: absolute;
		top: 0;
	}
	.content{
		background-color: #f9f9f9;
		height: 100%;
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: -1;
	}
	page {
		height: 100%;
	}
	.popup{
		background-color: #fff;
		width: 600rpx;
		font-size: 50rpx;
		z-index: 1;
		max-height: 85%;
		overflow: auto;
		box-shadow: 0 5px 7px 0 rgb(0 0 0 / 12%)
	}
	.popup-header{
		background-color: rgb(68,114,196);
		text-align: center;
		padding: 20rpx 0 ;
	}
	.popup-btn {
		font-size: 30rpx;
		color: #fff;
		padding-left: 40rpx;
		padding-right: 40rpx;
		background-color: rgb(68, 114, 196);
		margin-left: 40rpx;
		margin-right: 40rpx;
	}
	.uni-form-item {
		display: flex;
		align-items: center;
		padding-top: 20px;
		justify-content: center;
	}
	.popup-title {
		font-size: 30rpx;
		width: 60px;
		text-align: right;
	}
	.uni-input {
		font-size: 25rpx;
		border: 1px solid;
		padding: 20rpx 30rpx;
	}
	.uni-form-item.form-item-bottom{
		padding-bottom: 40rpx;
	}
	.chooseBtn{
		font-size: 30rpx;
		width: 438px;
	}
	.radio-group{
		width: 341px;
		display: flex;
	}
	.uni-list-cell{
		display: flex;
		align-items: center;
	}
</style>
