<template>
	<view style="height: 100%">
		<!-- pages/template/home/home.wxml -->

		<cu-custom :noFixed="true" :isLucency="true">
			<view slot="content"><text class="text-white text-xl">云数币</text></view>
		</cu-custom>

		<!-- 背景图 -->
		<image src="/static/images/9.png" mode="widthFix" class="bg-img-new"></image>

		<!-- 页面 -->
		<scroll-view scroll-y class="scrollPage">
			<view class="k-line-container">
			    <view class="menu-list">
			      <view class="menu-item active">实时</view>
			      <view class="menu-item">日K</view>
			    </view>
			    <view class="chart-container">
			       <uni-ec-canvas canvas-id="mychart-candlestick" width="100%" height="400px"></uni-ec-canvas>
			    </view>
			  </view>
			<view class="cu-tabbar-height"></view>
		</scroll-view>
	</view>
</template>

<script>
const app = getApp();
import * as echarts from 'echarts';

export default {
  data() {
    return {
      StatusBar: app.globalData.StatusBar,
      CustomBar: app.globalData.CustomBar,
      cardCur: 0,
      loading: false,
      legal_id: 0,
      currency_id: 0,
      symbol: "Loading",
      klineShow: false,
    };
  },
  options: {
    addGlobalClass: true
  },
  props: {},
  methods: {
    cardSwiper(e) {
      this.setData({
        cardCur: e.detail.current
      });
    },
    jumpTo(e) {
      return uni.navigateTo({
        url: e.currentTarget.dataset.page
      });
    },
    falseFun() {
      console.log('占位：函数 false 未声明');
    },
    newData: function (obj) {
      let newObj = Object.assign({}, this.dealInfo, obj);
      this.dealInfo = newObj;
    },
  },
  created: function() {},
};

function initChart(canvas, width, height, dpr) {
  const chart = echarts.init(canvas, null, {
    width: width,
    height: height,
    devicePixelRatio: dpr
  });

  const option = {
    xAxis: {
      data: ['2017-10-24', '2017-10-25', '2017-10-26', '2017-10-27']
    },
    yAxis: {},
    series: [
      {
        type: 'candlestick',
        data: [
          [20, 34, 10, 38],
          [40, 35, 30, 50],
          [31, 38, 33, 44],
          [38, 15, 5, 42]
        ]
      }
    ]
  };

  chart.setOption(option);
  return chart;
}

</script>
<style>
	/* pages/template/home/home.wxss */

	.k-line-container {
		padding: 10px;
	}

	.menu-list {
		display: flex;
		justify-content: flex-start;
		gap: 15px;
	}

	.menu-item {
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 8px;
	}

	.menu-item.active {
		background-color: #f0f0f0;
	}

	.chart-container {
		height: 300px;
	}
</style>