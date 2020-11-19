<template>
	<view class="content">
		<!--论滚标题-->
		<view class="swiper-banner">
			<swiper  indicator-dots="true" autoplay="true" interval="5000">
			  <swiper-item><image src="../../static/img/banner1.jpg"></image></swiper-item>
			  <swiper-item><image src="../../static/img/banner2.jpg"></image></swiper-item>
			</swiper>
		</view>
			
		<view class="user">
			<view class="title" v-if="user" >
				您好 {{user.name}}。
			</view>
			<view class="title" v-if="!user">
				<text>您好 游客。</text>
			</view> 		
		</view>
		<view class="line"></view>
		<view class="main">
			<view class="main-row">
				<view class="main-col">
					<view class="main-btn">
						<image src="../../static/img/团队.png"></image>
						<text>团队</text>
						
					</view>					
				</view>
				<view class="main-col">
					<view class="main-btn">
						<image src="../../static/img/团队.png"></image>
						<text>人员</text>
						
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
		            user:null
		        }
		    },
		onLoad() {
			this.guideToLogin();
		},
		methods: {
			guideToLogin() {
				this.user = uni.getStorageSync("user");
				if(!this.user){
					uni.showModal({
						title: '未登录',
						content: '您未登录，需要登录后才能继续',
						showCancel: true,
						success: (res) => {
							if (res.confirm) {
								this.jumpTar();
							}
						}
					});
				}
				
			},
			getDevice(){
					console.log(uni.getSystemInfoSync().platform)
					 switch(uni.getSystemInfoSync().platform){
					    case 'android':
					       console.log('运行Android上')
							return 'android';
					    case 'ios':
					       console.log('运行iOS上')
							return 'ios';
						case 'devtools':
							  console.log('运行开发工具上')
							return 'weixin';
						case 'other':
							console.log('运行h5上')
							return 'html';
					    default:
					       console.log('未知')
							return 'unknown';
					
					}
			},
			jumpTar(){
				let device = this.getDevice();
				if(device == 'weixin'){
					uni.redirectTo({
						url: '../login/login'
					});
				}else{
					uni.navigateTo({
						url: '../login/login'
					});
				}
			}
		}

	}
</script>

<style>
	@import url("main.css");
</style>
