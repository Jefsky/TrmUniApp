<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view>
		<view class="uni-form-item uni-column">
			<input class="uni-input" focus :placeholder="uni_input" @input="onKeyIdInput"/>
		</view>
		<view class="uni-btn-v">
			<button type="primary" @click="search">查询</button>
			<button type="primary" @click="qrcode">扫码</button>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: '',
				title: 'Hello',
				uni_input: '请输入运单号',
			}
		},
		onLoad() {

		},
		methods: {
			search: function (e) {
				uni.navigateTo({
					url: '../result/result?id='+this.id,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			onKeyIdInput: function (e) {
				this.id = e.target.value;
			},
			qrcode: function () {
				uni.scanCode({
					success: function (res) {
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
						uni.navigateTo({
							url: '../result/result?id='+res.result,
							success: res => {},
							fail: () => {},
							complete: () => {}
						});
					},
					
				});
				
			}
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
