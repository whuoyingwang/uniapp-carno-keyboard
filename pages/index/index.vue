<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
<!-- 		<view class="text-area">
			<text class="title">{{title}}</text>
		</view> -->
		<view class="input-cell">
			<view class="label">车牌：</view>
			<input :value="carNo" disabled @click="showCarNo" placeholder="请输入车牌" class="ainput"/>
		</view>

		<carnoKeyboard :showKeyboard.sync="modalShow" @kInput="onInput" @kDelete="onDelete" @kConfirm="onConfirm" @kClose="onClose"></carnoKeyboard>
	</view>
</template>

<script>
	import carnoKeyboard from '@/components/carno-keyboard/carno-keyboard.vue'
	export default {
		data() {
			return {
				carNo: '',
				modalShow: false
			}
		},
		components: {carnoKeyboard},
		methods: {
			showCarNo () {
				this.modalShow = true
			},
			onInput (item) {
				this.carNo += item
			},
			onDelete () {
				this.carNo = this.carNo.substr(0, this.carNo.length - 1)
			},
			onConfirm () {
				uni.showModal({
					content: this.carNo,
					showCancel: false
				})
			},
			onClose () {
				this.modalShow = false
			}
		}
	}
</script>

<style lang="less" scoped>
	.content {
		height: 100vh;
		width: 100vw;
		background-color: #F1F1F1;
	}
	.input-cell{
		display: flex;
		height: 80rpx;
		line-height: 80rpx;
		border-bottom: 1px solid #F1F1F1;
		background-color: #FFFFFF;
		font-size: 14px;
		.ainput {
			height: 80rpx;
			line-height: 80rpx;
			width: 550rpx;
		}
		.label {
			padding-left: 20rpx;
			width: 200rpx;
		}
	}

</style>
