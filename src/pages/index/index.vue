<template>
	<view class="content">
		<image class="logo" src="/static/index.png"></image>
		<view>
			<text class="title">{{hitokotoText}}</text>
		</view>
	</view>
</template>

<script>
import {uniGrid} from '@dcloudio/uni-ui'
import {uniGridItem} from '@dcloudio/uni-ui'
import {uniGroup} from '@dcloudio/uni-ui'

export default {
	components: {
		uniGrid,
		uniGridItem,
		uniGroup
	},
	data() {
		return {
			title: 'ToysTool Index',
			hitokotoText: '...',
			url: {
				hitokoto: 'https://v1.hitokoto.cn/'
			}
		}
	},
	onLoad() {
		this.init()
	},
	methods: {
		init () {
			let that = this
			uni.request({
				url: that.url.hitokoto,
				data: {
				},
				header: {
				},
				success: (res) => {
					that.hitokotoText = res.data.hitokoto
					setTimeout(this.jumpHome, 1500)
				}
			})
		},
		jumpHome () {
			console.log('jump home page')
			uni.redirectTo({
				url: '/pages/home/index',
				success: (res) => {
					console.log('success', res);
				},
				fail: (res) => {
					uni.showToast({
						icon: 'none',
						title: res.errMsg,
						duration: 3000
					})
				}
			})
		}
	}
}
</script>

<style>
	.content {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background: #e6e6e6;
	}

	.logo {
		height: 555rpx;
		width: 555rpx;
		margin: 0rpx auto 50rpx auto;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		width: 85%;
		font-size: 12rpx;
		color: #7979df;
	}
</style>
