<template>
    <view class="main">
        <view class="step-view">
            <uni-forms ref="baseForm" :rules="rules" class="step-form" :modelValue="baseForm">
                <uni-forms-item label-width="50" label-align="right" label="账号" class="step-form-items" required name="username">
                    <uni-easyinput v-model="baseForm.username" placeholder="请输入小米运动账号" />
                </uni-forms-item>
                <uni-forms-item label-width="50" label-align="right" label="密码" class="step-form-items" required name="password">
                    <uni-easyinput v-model="baseForm.password" placeholder="请输入小米运动密码" />
                </uni-forms-item>
                <uni-forms-item label-width="50" label-align="right" label="步数" class="step-form-items" required name="step">
                    <view style="display: flex;">
                        <uni-easyinput style="margin-right: 10px;" v-model="baseForm.step" placeholder="请输入步数" />
                        <button size="mini" @click="randomStep">Roll一下</button>
                    </view>
                </uni-forms-item>
            </uni-forms>
        </view>
        <view class="step-view button-view">
            <button class="button-view-item" type="primary" @click="submit('baseForm')">提交</button>
            <button class="button-view-item" type="info" @click="formReset">重置</button>
        </view>
        <uni-section title="注意事项：" type="line"></uni-section>
        <view>
            <view class="ps-content">
                <ul>
                    <li>1、从<span>应用商店</span> 或者<span>浏览器</span> 下载<span>小米运动App</span>, 打开软件并输入手机号登录</li>
                    <li>2、请自行注册<span>小米运动app</span> 账号, 不要使用<span>小米账号</span> 登陆
                    <li>3、不要使用<span>第三方账号</span>登录</li>
                    <li>4、登陆之后选择 <span>第三方同步</span></li>
                    <li>5、绑定需要同步的第三方应用</li>
                    <li>6、小米运动app的修改数据同步较慢, 请直接打开第三方app查看同步结果</li>
                    <li>7、本修改并不保证<span>每次</span>都能修改成功, 不成功时请多尝试几次, 且不保证<span>有效期</span></li>
                    <li>8、本项目仅供<span>学习</span>使用, 代码已开源在<span>github</span>上, 请下载后<span>24h内删除</span></li>
                    <li>9、https://github.com/niushuai233/mi-sport-change-java</li>
                </ul>
            </view>
        </view>
    </view>
</template>
<script>
import {uniForms} from '@dcloudio/uni-ui'
import {uniFormsItem} from '@dcloudio/uni-ui'
import {uniEasyinput} from '@dcloudio/uni-ui'
import {uniIcons} from '@dcloudio/uni-ui'
import {uniSection} from '@dcloudio/uni-ui'
export default {
    components: {
		uniForms,
        uniFormsItem,
        uniEasyinput,
        uniIcons,
        uniSection
	},
    data() {
        return {
            baseForm: {
                username: '',
                password: '',
                step: '',
            },
            // 校验规则
            rules: {
                username: {
                    rules: [{
                        required: true,
                        errorMessage: '账号不能为空'
                    }]
                },
                password: {
                    rules: [{
                        required: true,
                        errorMessage: '密码不能为空'
                    }]
                },
                step: {
                    rules: [{
                        required: true,
                        errorMessage: '步数不能为空'
                    }, {
                        format: 'number',
                        errorMessage: '步数只能输入数字'
                    }]
                }
            },
            url: {
                stepBiz: 'https://service.niushuai.cc/sport/mi/stepChange/change',
                stepBizLocal: 'http://localhost:9999/sport/mi/stepChange/change',
            }
        }
    },
    methods: {
        // 表单重置
        formReset: function(event) {
            this.baseForm.username = ''
            this.baseForm.password = ''
            this.baseForm.step = ''
            uni.showToast({
                title: '已重置'
            })
        },
        submit(ref) {
            this.$refs[ref].validate().then(res => {
                this.post(res)
            }).catch(err => {
                console.log('err', err);
            })
        },
        post(data) {
            let that = this
            uni.showLoading({
                title: '',
                mask: true
            });
            data.stepType = 'MI'
            data.timeStamp = new Date().getTime()
            uni.request({
				url: that.url.stepBizLocal,
				data: data,
                method: 'POST',
				header: {
				},
				success: (res) => {
                    uni.showToast({
                        title: res.data.msg
                    })
				},
                fail: (res) => {
                    console.error('change fail', res)
                    uni.showToast({
                        title: res.errMsg
                    })
                },
                complete: (res) => {
                    uni.hideLoading()
                }
			})
        },
        randomStep () {
            this.baseForm.step = Math.round(13000 + Math.random() * 5000);
        }
    }
}
</script>
<style>
.main {
    height: 400px;
}
.step-view {
    margin-top: 30px;
}

.step-form {
    padding: 3px 10px 0px 3px;
}

.step-form-items {
    width: 100%;
}

.button-view {
    display: flex;
}
.button-view-item {
    width: 45%;
}
.ps-content {
    font-size: 12px;
}
.ps-content span {
    font-style: italic;
    color: red;
}
</style>
