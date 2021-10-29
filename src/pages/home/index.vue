<template>
    <view>
        <view class="uni-padding-wrap">
            <view class="page-section swiper">
                <view class="page-section-spacing">
                    <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
                        <swiper-item>
                            <cover-image class="controls-play img" src="/static/banner/best.png"></cover-image>
                        </swiper-item>
                        <swiper-item>
                            <cover-image class="controls-play img" src="/static/banner/fat.png"></cover-image>
                        </swiper-item>
                        <swiper-item>
                            <cover-image class="controls-play img" src="/static/banner/yesconfirm.png"></cover-image>
                        </swiper-item>
                    </swiper>
                </view>
            </view>
        </view>
        <uni-group title="应用" top="20">
            <view class="application-body">
                <!-- 因为swiper特性的关系，请指定swiper的高度 ，swiper的高度并不会被内容撑开-->
                <swiper class="swiper" :indicator-dots="true">
                    <swiper-item>
                        <uni-grid :column="3" :highlight="true" @change="applicationChange">
                            <uni-grid-item v-for="(item, index) in list" :index="index" :key="index">
                                <view class="grid-item-box">
                                    <image :src="item.url" class="image" mode="aspectFill" />
                                    <text class="text">{{ item.text }}</text>
                                </view>
                            </uni-grid-item>
                        </uni-grid>
                    </swiper-item>
                </swiper>
            </view>
        </uni-group>

        <uni-group title="工具">
        </uni-group>
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
		uniGroup,
	},
    data() {
        return {
            background: ['color1', 'color2', 'color3'],
            indicatorDots: true,
            autoplay: true,
            interval: 2000,
            duration: 500,
            list: [{
                key: 'stepChange',
                url: '/static/c1.png',
                text: '步数修改',
                badge: '0',
                type: "primary"
            }]
        }
    },
    onLoad() {
    },
    methods: {
        applicationChange (item) {
            let list_item = this.list[item.detail.index]
            console.log(list_item)
            if (list_item.key == 'stepChange') {
                this.jumpPage('/pages/stepchange/index')
            }
        },
        jumpPage (_url) {
            uni.redirectTo({
				url: _url,
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
<style scoped>
    .grid-item-box {
        font-size: 16px;
    }
    .grid-item-box image {
        width: 50px;
        height: 50px;
    }
    .application-body .swiper {
        height: 128px;
    }
</style>