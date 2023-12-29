<template>
	<view class="cate-wrap">
		<view class="btn-wrap">
			<u-radio-group 
			    v-model="category"
			    placement="row"
				class="btn-wrap"
			>
				<u-radio
				  v-for="(item, index) in categoryList"
				  :key="index"
				  :name="item.key"
				  :label="item.name"
				></u-radio>
			</u-radio-group>
			<!-- 				  :label="item.name" -->
			<!-- 				  :customStyle="{marginBottom: '8px'}" -->
			<!--
			<view class="btn-item">
				<u-button type="primary" text="确定">IT圈</u-button>
			</view> -->
		</view>
		<view class="op-wrap">
			<view class="op-time">
				<text>时长：</text>
				<text>{{ time }}s</text>
				<u-icon @click="editTime" name="edit-pen"></u-icon>
				<u-action-sheet :actions="timeList" @select="selectClick" :show="show" cancelText="取消" @close="cancel"></u-action-sheet>	
			</view>
			<view class="">
				<u-button type="primary" text="确定" @click="start">开始游戏</u-button>
			</view>
		</view>
		<u-popup :show="tipShow" @open="openTip" mode="center" :round="10">
			<view>
				<p>1.回答者将手机横屏并正对朝向表演者</p>
				<p>2.表演者表演或描述看到的词语，不能说出题目中的字</p>
				<p>3.表演者示意回答者结果，回答者操作手机换词（下翻正确，上翻跳过）</p>
				<u-button type="primary" text="我知道了" @click="goGame"></u-button>
			</view>
		</u-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				time: 90,
				tipShow: false,
				show: false,
				timeList: [
					{
						name: '60s',
						value: 60,
						color:'#ffaa7f',
						fontSize:'20'
					},
					{
						name: '90s',
						value: 90,
						color:'#ffaa7f',
						fontSize:'20'
					},
					{
						name: '120s',
						value: 120,
						color:'#ffaa7f',
						fontSize:'20'
					}
				],
				category: 'hodgepodge',
				categoryList: [
					{
						key: 'hodgepodge',
						name: '大杂烩',
					},
					{
						key: 'video',
						name: '我爱电影',
					},
					{
						key: 'foodie',
						name: '吃货天堂',
					},
					{
						key: 'act',
						name: '表演卡',
					},{
						key: 'music',
						name: '我是麦霸',
					},{
						key: 'star',
						name: '大明星',
					},{
						key: '90',
						name: '90后',
					},{
						key: '80',
						name: '80后',
					},{
						key: 'it',
						name: 'IT圈',
					},
				],
			};
		},
		methods: {
			editTime() {
				this.show = true;
			},
			selectClick(data) {
				console.log(data);
				const { value } = data;

				this.time = value;
			},
			cancel() {
				this.show = false;
			},
			start() {
				console.log(this.category);
				this.openTip();
			},
			openTip() {
				this.tipShow = true;
			},
			closeTip() {
				this.tipShow = false;
			},
			goGame() {
				this.closeTip();
				const cateId = this.category;
				const time = this.time;

				uni.navigateTo({
					url: `/pages/guess-category/category-process/index?cateId=${cateId}&time=${time}`,
				})
			}
		},
	}
</script>

<style lang="scss">
	.u-radio-group {
		flex-wrap: wrap;
	}
	.u-radio {
		flex: 1 0 calc(33.33% - 10px) !important; /* 计算宽度，按照每行三个盒子 */
		height: 100px;
		margin: 5px;
		background-color: lightgray;
		border-radius: 20px;
	}
	.cate-wrap {
		.btn-wrap {
			// display: flex;
			// flex-wrap: wrap;
			
			.btn-item {
				flex: 1 0 calc(33.33% - 10px); /* 计算宽度，按照每行三个盒子 */
				height: 100px;
				margin: 5px;
				background-color: lightgray;
			}
		}
		.op-wrap {
			display: flex;
			flex-direction: column;
			align-items: center;
			.op-time {
				display: flex;
			}
		}
	}
</style>