<template>
	<view class="cityContent">
		<navigator class="conlation" url="/pages/selectCity/selectCity">
			<view class="iconfont icondingwei conlation-left">
				自动定位: {{cCity}}
			</view>
			<navigator url="/pages/selectCity/selectCity" class="conlation-right">
				切换 <text class="iconfont iconyoujiantou"></text>
			</navigator>
		</navigator>

		<view class="video-list">
			<span v-for="(item,index) in list" :key="index">
				<view class="item">
					<view class="video">
						<video :src="path(item.src)" controls style="width: 100%; height: 100%;"></video>
					</view>
					<view class="image-box">
						<image src="../static/me.jpg" class="image"></image>
					</view>
				</view>
			</span>
		</view>
	</view>
</template>

<script>
	export default {
		props: [
			"list"
		],
		data() {
			return {
				cCity: '上海'
			};
		},
		created() {
			uni.getStorage({
				key: 'city',
				success: (res) => {
					this.cCity = res.data
				}
			})
		},
		methods:{
			path(src) {
				// 如果不是用数据库的话，要改下这个path
				return `http://localhost:8080/static/video/${src}.mp4`
			}
		}
	}
</script>

<style>
	.cityContent {
		padding: 4px;
		width: 100%;
		background-color: #000000;
	}

	.conlation {
		width: 100%;
		height: 40px;
		margin-top: 60px;
		overflow: hidden;
		color: #aaaaaa;
		font-size: 14px;
		line-height: 14px;
	}

	.conlation-right {
		float: right;
		padding-right: 15px;
	}

	.conlation-left {
		float: left;
		padding-left: 15px;
	}

	.video-list {
		width: 100%;
		overflow: auto;
		background: #000000;
	}

	.item {
		width: 50%;
		float: left;
		position: relative;
	}

	.video {
		width: 92%;
		margin: 0 auto;
		height: 300px;
	}

	.image-box {
		position: absolute;
		bottom: 10px;
		right: 25px;

	}

	.image {
		width: 20px;
		height: 20px;
		border-radius: 50%;
	}
</style>
