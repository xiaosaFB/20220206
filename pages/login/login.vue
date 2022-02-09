<template>
  <view class="content">
    <view class="header">
      <image src="../../static/shilu-login/logo.png"></image>
    </view>

    <view class="list">
      <view class="list-call">
        <image class="img" src="/static/shilu-login/1.png"></image>
        <input class="sl-input" v-model="phone" type="number" maxlength="11" placeholder="输入手机号" />
      </view>
      <view class="list-call">
        <image class="img" src="/static/shilu-login/2.png"></image>
        <input class="sl-input" v-model="password" type="text" maxlength="32" placeholder="输入密码" password="true" />
      </view>

    </view>

    <view class="button-login" hover-class="button-hover" @tap="bindLogin()">
      <text>登录</text>
    </view>

    <view class="agreenment">
      <navigator url="forget" open-type="navigate">忘记密码</navigator>
      <text>|</text>
      <navigator url="reg" open-type="navigate">注册账户</navigator>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        phone: '',
        password: ''
      };
    },
    methods: {
      bindLogin() {
		  if (this.phone.length != 11) {
			  uni.showToast({
				icon: 'none',
				title: '手机号不正确'
			  });
			return;
		} else if(this.password.length < 6) {
			  uni.showToast({
				icon: 'none',
				title: '密码不正确'
			  });
			  return;
		} else if (this.phone != '17712341234' || this.password != '123456') {
			uni.showToast({
				icon: 'none',
				title: '请仔细检查账号密码是否正确'
			});
			return;
		} else if(this.phone == '17712341234' || this.password == '123456'){
			uni.setStorageSync('login_key',1)
			//成功后的逻辑
			// uni.navigateBack();
			uni.reLaunch({
			    url: '../index/index?index=0'
			});
		}
      }
    }
  }
</script>

<style>
  .content {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .header {
    width: 281rpx;
    height: 281rpx;
    background: rgba(0, 85, 255, 1.0);
    box-shadow: 0rpx 12rpx 13rpx 0rpx rgba(0, 85, 255, 0.5);
    border-radius: 50%;
    margin-top: 30rpx;
    margin-left: auto;
    margin-right: auto;
  }

  .header image {
    width: 281rpx;
    height: 281rpx;
    border-radius: 50%;
  }

  .list {
    display: flex;
    flex-direction: column;
    padding-top: 150rpx;
    padding-left: 20rpx;
    padding-right: 20rpx;
  }

  .list-call {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height: 100rpx;
    color: #333333;
    border-bottom: 0.5px solid #e2e2e2;
  }

  .list-call .img {
    width: 40rpx;
    height: 40rpx;
  }

  .list-call .sl-input {
    flex: 1;
    text-align: left;
    font-size: 32rpx;
    margin-left: 16rpx;
  }

  .button-login {
    color: #FFFFFF;
    font-size: 34rpx;
    width: 80%;
    height: 100rpx;
    background: linear-gradient(-200deg, rgba(0, 85, 255, 1.0), rgba(0, 85, 255, 0.3));
    box-shadow: 0rpx 0rpx 13rpx 0rpx rgba(164, 217, 228, 0.2);
    border-radius: 50rpx;
    line-height: 100rpx;
    text-align: center;
    margin-left: auto;
    margin-right: auto;
    margin-top: 100rpx;
  }

  .button-hover {
    background: linear-gradient(-200deg, rgba(0, 85, 255, 1.0), rgba(0, 85, 255, 0.3));
  }

  .agreenment {
    display: flex;
    flex-direction: row;
    justify-content: right;
    align-items: center;
    font-size: 30rpx;
    margin-top: 80rpx;
	margin-right: 20rpx;
    color: #0055ff;
    text-align: center;
    height: 40rpx;
    line-height: 40rpx;
  }

  .agreenment text {
    font-size: 24rpx;
    margin-left: 15rpx;
    margin-right: 15rpx;
  }
</style>
