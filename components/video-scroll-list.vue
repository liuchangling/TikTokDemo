<template>
	<view class="scorllList">
		<view class="videoList">
			<scroll-view scroll-y="true" style="height: 100%;" @scroll="scroll">
				<view class="videoItem" v-for="(item,index) in list" :key="item.id">
					<view class="authorInfo">
						<image src="../static/me.jpg" class="authorImg"></image>
						<text class="authorName">{{item.author}}</text>
						<icon class="iconfont iconshenglvehao share"></icon>
					</view>

					<view class="videoBox">
						<text class="title">
							{{item.title}}
						</text>

						<video-scroll-player :item="item" ref="player" :index="index"></video-scroll-player>

						<view class="music-box">
							<view class="music">
								{{item.musicAuthor}}@{{item.music}}
							</view>
						</view>
					</view>
					<view class="dataBox">
						<view class="data-left">
							<text>3小时前</text>
						</view>
						<view class="data-right">
							<icon class="iconfont iconaixin icon">
								<text>赞</text>
							</icon>

							<icon class="iconfont iconpinglun icon">
								<text>评论</text>
							</icon>

							<icon class="iconfont iconfenxiang icon">
								<text>分享</text>
							</icon>
						</view>
					</view>
					<view class="comment">
						<text class="loveNumber">1.1w评论过</text>
						<view class="commentBox">
							<icon class="iconfont iconqianbi" style="float: left;"></icon>
							<input type="text" value="" placeholder="添加评论..." class="inputComment" />
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	import videoScrollPlayer from './video-scroll-player.vue'

	let timer
	export default {
		components: {
			videoScrollPlayer
		},
		props: [
			'list'
		],
		data() {
			return {
				index: 0
			};
		},
		methods: {
			scroll(res) {
				clearTimeout(timer)
				timer = setTimeout(() => {
					this.index = Math.floor(res.detail.scrollTop / 550)
				}, 300);

			},
			isValidIndex(num) {
				return num >= 0 && num < this.list.length
			}
		},
		watch: {
			index() {
				if (this.isValidIndex(this.index)) {
					this.$refs.player[this.index].play()
				}

				for (let i = this.index - 5; i < this.index + 5; i++) {
					if (i != this.index) {
						if (this.isValidIndex(i)) {
							this.$refs.player[i].pause()
						}
					}
				}
			}
		}
	}
</script>

<style>
	.scorllList {
		width: 100%;
		height: 100%;
	}

	.videoItem {
		padding: 0 15px;
		width: 90%;
		height: 100%;
	}

	.authorInfo {
		height: 35px;
		line-height: 35px;

	}

	.authorImg {
		width: 35px;
		height: 35px;
		border-radius: 50%;
		float: left;
	}

	.authorName {
		font-size: 16px;
		margin-left: 10px;
		text-align: center;
	}

	.share {
		float: right;
		font-size: 25px;
		margin-right: 5px;
	}

	.videoBox {
		width: 100%;
		height: 370px;
	}

	.music-box {
		z-index: 8;
		position: relative;
		bottom: 30px;
		font-size: 14px;
		width: 100px;
		overflow: hidden;
	}

	.music {
		width: 200px;
		animation: XLeft 4s linear infinite;
	}

	.title {
		width: 100%;
		font-size: 13px;
		margin-top: 25px;
		line-height: 25px;
	}

	.dataBox {
		height: 25px;
		margin-top: 40px;
		line-height: 25px;
	}

	.data-left {
		float: left;
		font-size: 15px;
		color: #AAAAAA;
		font-size: 11px;
	}

	.data-right {
		float: right;
	}

	.icon {
		float: right;
		font-size: 11px;
		padding: 0 10px;
	}

	.loveNumber {
		width: 100%;
		height: 25px;
		font-size: 15px;
		line-height: 15px;
		color: #AAAAAA;
		margin: 10px 0;
	}

	.commentBox {
		height: 100px;
		line-height: 25px;
		background-color: #1A1A1A;
	}

	.inputComment {
		margin-left: 30px;
		font-size: 15px;
	}

	.videoList {
		width: 100%;
		height: 100%;
	}


	@keyframes XLeft {
		0% {
			transform: translate3d(80%, 0, 0);
		}

		100% {
			transform: translate3d(-80%, 0, 0);
		}
	}
</style>
