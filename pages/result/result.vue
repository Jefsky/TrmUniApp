<template>
	<view class="content">
		<view class="text-box" scroll-y="true">
			<text class="uni-h3 uni-page-head-title">运单{{id}}物流状态</text>
		</view>
		<view class="uni-list">
			<uni-list class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in list" :key="index">
				<uni-list-item v-if="index == 0" class="uni-h4" :title="item.w_place+'-'+item.w_content" :note="item.w_date" show-arrow="false" show-extra-icon="true" :extra-icon="iconin"></uni-list-item>
				<uni-list-item v-else class="uni-h4" :title="item.w_place+'-'+item.w_content" :note="item.w_date" show-arrow="false" show-extra-icon="true" :extra-icon="icon"></uni-list-item>
			</uni-list>
		</view>
	</view>
</template>

<script>
	import uniList from '@/components/uni-list/uni-list.vue'
	import uniListItem from '@/components/uni-list-item/uni-list-item.vue'
	import uniIcon from "@/components/uni-icon/uni-icon.vue"
	export default {
		components: {uniList,uniListItem,uniIcon},
		data() {
			return {
				list: [],
				id: '',
				icon: {color: '#ddd',size: '22',type: 'location-filled'},
				iconin: {color: 'red',size: '22',type: 'location-filled'},
			}
		},
		onLoad(e){
			var id = e.id;
			this.id = id;
			uni.showLoading({
				title: '查询中...'
			});
			uni.request({
				url: 'http://www.hu1tong.com/index.php/index/query?id='+id,
				method: 'GET',
				data: {},
				success: res => {
					uni.hideLoading();
					this.list = res.data.data;
					if(this.list == 0){
						uni.showModal({
							title: '提示',
							content: '运单不存在或暂无物流信息',
							showCancel: false,
							success: function (res) {
								if (res.confirm) {
									uni.navigateBack();
								} 
							}
						});
					}
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
