<template>
	<!-- 为你推荐 -->
	<view class="hot-goods mx20 mb10" v-if="goodsList.length">
		<view class="goods-list x-f">
			<view class="goods-item" v-for="goods in goodsList" :key="goods.id"><shopro-goods-card :detail="goods" :isTag="true"></shopro-goods-card></view>
		</view>
	</view>
</template>

<script>
import shoproGoodsCard from '@/components/shopro-goods-card/shopro-goods-card.vue';
export default {
	components: {
		shoproGoodsCard
	},
	data() {
		return {
			listParams: {},
			goodsList: []
		};
	},
	props: {
		detail: {
			type: Object,
			default: null
		}
	},
	created() {
		if (this.detail.id) {
			this.listParams.category_id = this.detail.id;
			this.getGoodsList();
		}
		if (this.detail.ids) {
			this.listParams.goods_ids = this.detail.ids;
			this.getGoodsList();
		}
	},
	computed: {},
	methods: {
		// 商品列表
		getGoodsList() {
			let that = this;
			that.$api('goods.lists', this.listParams).then(res => {
				if (res.code === 1) {
					that.goodsList = res.data.data;
				}
			});
		}
	}
};
</script>

<style lang="scss">
// 为你推荐
.hot-goods {
	background: linear-gradient(#fff 200rpx, #f6f6f6 500rpx, #f6f6f6);
	border-radius: 20rpx;
	.goods-list {
		flex-wrap: wrap;
		width: 710rpx;
		.goods-item {
			margin-right: 20rpx;
			margin-bottom: 20rpx;
			width: 345rpx;
			box-shadow: 0px 0px 10rpx 4rpx rgba(199, 199, 199, 0.22);
			border-radius: 20rpx;
			&:nth-child(2n) {
				margin-right: 0;
			}
		}
	}
}
</style>
