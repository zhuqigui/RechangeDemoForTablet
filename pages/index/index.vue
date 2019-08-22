<template>
	<view>
		<view class="content">
			<image class="logo" src="/static/generate_111111.png"></image>
		</view>
		<view class="uni-flex uni-column slot-status">
			<!--text-area-->
			<view class="uni-flex uni-row">
				<!---->
				<view class="flex-item" v-bind:class="{uni_bg_red:hole1_message=='使用中'}">{{hole1_message}}</view>
				<view class="flex-item" v-bind:class="{uni_bg_red:hole2_message=='使用中'}">{{hole2_message}}</view>
				<view class="flex-item" v-bind:class="{uni_bg_red:hole3_message=='使用中'}">{{hole3_message}}</view>
			</view>
			<view class="uni-flex uni-row">
				<view class="flex-item" v-bind:class="{uni_bg_red:hole4_message=='使用中'}">{{hole4_message}}</view>
				<view class="flex-item" v-bind:class="{uni_bg_red:hole5_message=='使用中'}">{{hole5_message}}</view>
				<view class="flex-item" v-bind:class="{uni_bg_red:hole6_message=='使用中'}">{{hole6_message}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				hole_id: 6,
				message:'',
				intervalID:0,//
				hole1_message: '空闲',
				hole2_message: '空闲',
				hole3_message: '空闲',
				hole4_message: '空闲',
				hole5_message: '空闲',
				hole6_message: '空闲',
				'uni':uni,
			};
		},
		watch:{
			hole_id:function(nval, oval){
				console.log('hole_id值的变化 :' + oval + ' 变为 ' + nval + '!');
				// if (nval==1) {
				// 	if(this.message=='open'){
				// 		this.hole1_message = "充电中";
				// 	}else{
				// 		this.hole1_message = "空闲";
				// 	}
				// 	console.log("watch hole_id==1，hole3_message=="+this.hole1_message);
				// } else if (nval == 2) {
				// 	if(this.message=='open'){
				// 		this.hole2_message = "充电中";
				// 	}else{
				// 		this.hole2_message = "空闲";
				// 	}
				// 	console.log("watch hole_id==2，hole2_message=="+this.hole2_message);
				// } else if (this.hole_id == 3) {
				// 	if(this.message=='open'){
				// 		this.hole3_message = "充电中";
				// 	}else{
				// 		this.hole3_message = "空闲";
				// 	}
				// 	console.log("watch hole_id==3，hole3_message=="+this.hole3_message);
				// } else if (this.hole_id == 4) {
				// 	if(this.message=='open'){
				// 		this.hole4_message = "充电中";
				// 	}else{
				// 		this.hole4_message = "空闲";
				// 	}
				// 	console.log("watch hole_id==4，hole4_message=="+this.hole4_message);
				// } else if (this.hole_id == 5) {
				// 	if(this.message=='open'){
				// 		this.hole5_message = "充电中";
				// 	}else{
				// 		this.hole5_message = "空闲";
				// 	}
				// 	console.log("watch hole_id==5，hole5_message=="+this.hole5_message);
				// } else if (this.hole_id == 6) {
				// 	if(this.message=='open'){
				// 		this.hole6_message = "充电中";
				// 	}else{
				// 		this.hole6_message = "空闲";
				// 	}
				// 	console.log("watch hole_id==6，hole6_message=="+this.hole6_message);
				// }
			},
			hole1_message:function(nval, oval){
				console.log('hole1_message值的变化 :' + oval + ' 变为 ' + nval + '!');
			},
			hole2_message:function(nval, oval){
				console.log('hole2_message值的变化 :' + oval + ' 变为 ' + nval + '!');
			},
			hole3_message:function(nval, oval){
				console.log('hole3_message值的变化 :' + oval + ' 变为 ' + nval + '!');
			},
			hole4_message:function(nval, oval){
				console.log('hole4_message值的变化 :' + oval + ' 变为 ' + nval + '!');
			},
			hole5_message:function(nval, oval){
				console.log('hole5_message值的变化 :' + oval + ' 变为 ' + nval + '!');
			},
			hole6_message:function(nval, oval){
				console.log('hole6_message值的变化 :' + oval + ' 变为 ' + nval + '!');
			}
		},
		onLoad() {
			var that=this;
			uni.connectSocket({
				url: 'ws://39.106.217.14:8000/ws/keep_websocket_status/?facility_id=111111'
			});
			uni.onSocketOpen(function(res) {
				console.log('WebSocket连接已打开！');
			});
			uni.onSocketError(function(res) {
				console.log('WebSocket连接打开失败，请检查！');
			});
			uni.onSocketClose(function(res) {
				console.log('WebSocket 已关闭！');
			});
			uni.onSocketMessage(function(res) {
				console.log('收到服务器内容：' + res.data);
				var data = JSON.parse(res.data);
				that.hole_id= data.hole_id;
				var message= data.message;
				//console.log("hole_id==" +that.hole_id+",message=="+message);
				that.hole1_message=message['slots1'];
				that.hole2_message=message['slots2'];
				that.hole3_message=message['slots3'];
				that.hole4_message=message['slots4'];
				that.hole5_message=message['slots5'];
				that.hole6_message=message['slots6'];
				console.log("that.hole_id==" + that.hole_id+",hole1_message=="+that.hole1_message
							+",that.hole2_message=="+that.hole2_message
							+",that.hole3_message=="+that.hole3_message
							+",that.hole4_message=="+that.hole4_message
							+",that.hole5_message=="+that.hole5_message
							+",that.hole6_message=="+that.hole6_message
							);
			})
		},
		// onHide: () => {
		// 	
		// },
		methods: {
			click1:function(val){
				this.hole_id=val;
				//computedHoleMessage();
				console.log("click1 this.hole_id=1...");
			}
		},
	};
	
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 20upx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 20upx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}

	.uni-row {
		flex-direction: row;
	}
	.uni-column {
		flex-direction: column;
	}
	.uni-flex {
		display: flex;
		/* 		flex-direction: row; */
		width: 100%;
	}

	.slot-status {
		width: 100%;
		height: 300upx;
	}
	.flex-item {
		width: 30%;
		height: 130upx;
		text-align: center;
		line-height: 130upx;
		margin-left: 20upx;
		margin-bottom: 30upx;
		margin-top: 10upx;
		background-color:#09bb07;
		color: #fff;
	}
	/* 背景色 */
	.uni_bg_red {
		background-color: #f76260;
		color: #fff;
	}
</style>