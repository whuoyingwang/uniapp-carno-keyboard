<template>
	<view v-if="show">
		<view class="mask" @touchmove.stop.prevent="moveHandle" @click="close('mask')"></view>
		<view class="keyboardbox" @touchmove.stop.prevent="moveHandle" :class="ani">
			<view class="switch">
				<view class="keyboard-cell" @click="changeKeyBoard">
					<view :class="{ 'active': swIndex}">中</view> <view style="margin: 0 10rpx;">/</view> <view :class="{ 'active': !swIndex}">英</view>
				</view>
			</view>
			<view class="keyboard" >
				<template v-if="swIndex">
					<view class="keyboard-cell" v-for="(item, index) in provinceArr" :key="index" @click="choose(item)">{{ item }}</view>
				</template>
				<template v-else>
					<view class="keyboard-cell" v-for="(item, index) in strArr" :key="index"  @click="choose(item)">{{ item }}</view>
				</template>
				<view class="tools">
					<view class="tools-c" @click="delHandle">
						<image src="../../static/delete.png" class="del-img" mode="aspectFit"></image>
					</view>
					<view class="tools-c" @click="confirm">
						<view class="confirm">确认</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swIndex: true,
				provinceArr: ['桂', '粤', '京', '津', '渝', '沪', '冀', '晋', '辽', '吉', '黑', '苏', '浙', '皖', '闽', '赣', '鲁', '豫', '鄂', '湘',
					'琼', '川', '贵', '云', '陕', '甘', '青', '蒙', '宁', '新', '藏', '使', '领', '警', '学', '港', '澳'
				],
				strArr: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', 'A',
					'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', 'Z', 'X', 'C', 'V', 'B', 'N', 'M'
				],
				show: false,
				ani: ''
			}
		},
		props: {
			showKeyboard: {
				type: Boolean,
				default: false
			}
		},
		watch:{
			showKeyboard (newV) {
				console.log(newV)
				if (newV) {
					this.open()
				} else {
					this.close()
				}
			}
		},
		methods: {
			moveHandle(e) {
				// console.log('阻止蒙层下面元素滚动', e)
			},
			changeKeyBoard () {
				this.swIndex = !this.swIndex
			},
			choose(item) {
				// console.log('选择', item)
				this.$emit('onInput', item)
			},
			delHandle() {
				this.$emit('onDelete')
			},
			confirm() {
				this.$emit('onConfirm')
				this.close('mask')
			},
			open() {
				this.show = true
				setTimeout(() => {
					this.ani = 'top'
				}, 20)
			},
			close (type) {
				if (type == 'mask') {
					this.$emit('update:showKeyboard', false)
				}
				this.ani = ''
				setTimeout(() => {
					this.show = false
					this.swIndex = true // 输入框恢复中文选择
					this.$emit('onClose')
				}, 200)
			}
		}
	}
</script>

<style lang="less" scoped>
	.cell {
		font-size: 32rpx;
		color: #353535;
		height: 76rpx;
		width: 64rpx;
		line-height: 76rpx;
		text-align: center;
		background-color: #fff;
		margin-left: 10rpx;
		margin-bottom: 20rpx;
		box-shadow: 0 3rpx 2rpx 0 gray;
		border-radius: 5rpx;
		font-weight: 600;
		
		&:active {
			background-color: #d8d8d8;
		}
	}
	
	.mask{
		position: absolute;
		z-index: 50;
		height: 5000px;
		width: 750rpx;
		overflow: hidden;
		top: 0;
		left: 0;
		background-color: #000000;
		opacity: 0.5;
	}
	
	.keyboardbox{
		background-color: #dddddd;
		position: fixed;
		z-index: 52;
		left: 0;
		bottom: 0rpx;
		width: 100%;
		transition: all .2s;
		transform: translateY(100%);
		// height: 300rpx;
		.keyboard {
			display: flex;
			flex-wrap: wrap;
			justify-content: flex-start;
			.keyboard-cell {
				.cell()
			}
			
			.tools{
				width: 225rpx;
				display: flex;
				position: absolute;
				bottom: 0;
				right: 0;
				.tools-c {
					.cell();
					display: flex;
					width: 100rpx;
					align-items: center;
					justify-content: center;
					.del-img {
						height: 66rpx;
						width: 75rpx;
					}
				}
			}
		}
		
		.switch {
			display: flex;
			justify-content: flex-end;
			padding-top: 20rpx;
			.keyboard-cell {
				.cell();
				width: 140rpx;
				margin-right: 10rpx;
				margin-left: 0rpx;
				display: flex;
				justify-content: center;

				.active{
					color: #4CD964;
				}
			}
		}
	}
	.top{
		// bottom: 0rpx;
		// transition: all .2s;
		transform: translateY(0);
	}
</style>
