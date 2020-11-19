<template>
	<view class="content">
		<view class="login-type">
			<view v-for="(item,index) in loginTypeList" :key="index" @click="loginType = index" :class="{act: loginType === index}"
			 class="login-type-btn">{{item}}</view>
		</view>
		<view class="input-group" v-if="loginType === 0">
			企业目标
		</view>
		<view class="input-group" v-else-if="loginType === 1">
			团队目标
		</view>
		<view class="input-group" v-else>
			个人目标
		</view>
	 <view id="main" style="width: 720rpx;height: 600rpx;"></view>
	</view>
</template>

<script>	
	import {
		mapState,
		mapMutations
	} from 'vuex'
	import mInput from '../../components/m-input.vue'

	export default {
		components: {
			mInput
		},
		data() {
			return {
				loginType: 0,
				loginTypeList: ['企业目标', '团队目标', '个人目标'],
				mobile: '',
				code: '',
				providerList: [],
				hasProvider: false,
				username: '',
				password: '',
				positionTop: 0,
				isDevtools: false,
				codeDuration: 0,
				  name: '',
				                charts: '',
				            /*  opinion: ["1", "3", "3", "4", "5"],*/
				                opinionData: ["3", "2", "4", "4", "5"]

			}
		},
		computed: mapState(['forcedLogin']),
		 methods: {
		            drawLine(id) {
		                this.charts = echarts.init(document.getElementById(id))
		                this.charts.setOption({
		                    tooltip: {
		                        trigger: 'axis'
		                    },
		                    legend: {
		                        data: ['近七日收益']
		                    },
		                    grid: {
		                        left: '3%',
		                        right: '4%',
		                        bottom: '3%',
		                        containLabel: true
		                    },
		 
		                    toolbox: {
		                        feature: {
		                            saveAsImage: {}
		                        }
		                    },
		                    xAxis: {
		                        type: 'category',
		                        boundaryGap: false,
		                    data: ["1","2","3","4","5"]
		                    
		                    },
		                    yAxis: {
		                        type: 'value'
		                    },
		 
		                    series: [{
		                        name: '近七日收益',
		                        type: 'line',
		                        stack: '总量',
		                        data: this.opinionData
		                    }]
		                })
		            }
		        },
		        //调用
		        mounted() {
		            this.$nextTick(function() {
		                this.drawLine('main')
		            })
		        }

	}
</script>

<style>
	.login-type {
		display: flex;
		justify-content: center;
	}

	.login-type-btn {
		line-height: 30px;
		margin: 0px 15px;
	}

	.login-type-btn.act {
		color: #0FAEFF;
		border-bottom: solid 1px #0FAEFF;
	}

	.send-code-btn {
		width: 120px;
		text-align: center;
		background-color: #0FAEFF;
		color: #FFFFFF;
	}

	.action-row {
		display: flex;
		flex-direction: row;
		justify-content: center;
	}

	.action-row navigator {
		color: #007aff;
		padding: 0 10px;
	}

	.oauth-row {
		display: flex;
		flex-direction: row;
		justify-content: center;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
	}

	.oauth-image {
		position: relative;
		width: 50px;
		height: 50px;
		border: 1px solid #dddddd;
		border-radius: 50px;
		margin: 0 20px;
		background-color: #ffffff;
	}

	.oauth-image image {
		width: 30px;
		height: 30px;
		margin: 10px;
	}

	.oauth-image button {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		opacity: 0;
	}
</style>
