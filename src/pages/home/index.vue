<template>
     <view>
        <uni-group title="分组1" top="20">
            <view>分组1 的内容</view>
            <view>分组1 的内容</view>
        </uni-group>

        <uni-group title="分组2">
            <view>分组2 的内容</view>
            <view>分组2 的内容</view>
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
        }
    },
    onLoad() {
    },
    methods: {
    }
}
</script>
