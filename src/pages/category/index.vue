<template>
  <view>
    <!-- 搜索 -->
    <search />
    <!-- 分类 -->
    <view class="category">
      <!-- 顶级分类 -->
      <view class="sup">
        <scroll-view scroll-y>
          <text :class="{'active':index===ac_index}" @tap="change(index)" v-for="(item,index) in list" :key="item.cat_id">{{item.cat_name}}</text>
          <!-- <text>热门推荐</text>
          <text>海外购</text>
          <text>苏宁房产</text>
          <text>手机相机</text>
          <text>电脑办公</text>
          <text>厨卫电器</text>
          <text>食品酒水</text>
          <text>居家生活</text>
          <text>厨房电器</text> -->
        </scroll-view>
      </view>
      <!-- 子级分类 -->
      <view class="sub">
        <scroll-view scroll-y>
          <!-- 封面图 -->
          <image src="http://static.botue.com/ugo/uploads/category.png" class="thumb"></image>
          <view class="children" v-for="one in list[ac_index].children" :key="one.cat_id">
            <view class="title">{{one.cat_name}}</view>
            <!-- 品牌 -->
            <view class="brands">
              <navigator :url="'/pages/list/index?query='+item.cat_name" v-for="item in one.children" :key="item.cat_id">
                <image :src="item.cat_icon"></image>
                <text>{{item.cat_name}}</text>
              </navigator>
              <!-- <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_2.jpg"></image>
                <text>海信</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_3.jpg"></image>
                <text>创维</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_4.jpg"></image>
                <text>夏普</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_5.jpg"></image>
                <text>TCL</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_6.jpg"></image>
                <text>PPTV</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_7.jpg"></image>
                <text>小米</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_8.jpg"></image>
                <text>长虹</text>
              </navigator> -->
            </view>
          </view>
          <!-- <view class="children">
            <view class="title">电视</view>
             品牌 
            <view class="brands">
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_1.jpg"></image>
                <text>曲面电视</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_2.jpg"></image>
                <text>海信</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_3.jpg"></image>
                <text>创维</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_4.jpg"></image>
                <text>夏普</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_5.jpg"></image>
                <text>TCL</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_6.jpg"></image>
                <text>PPTV</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_7.jpg"></image>
                <text>小米</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_8.jpg"></image>
                <text>长虹</text>
              </navigator>
            </view>
          </view> -->
          <!-- <view class="children">
            <view class="title">电视</view>
             品牌
            <view class="brands">
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_1.jpg"></image>
                <text>曲面电视</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_2.jpg"></image>
                <text>海信</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_3.jpg"></image>
                <text>创维</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_4.jpg"></image>
                <text>夏普</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_5.jpg"></image>
                <text>TCL</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_6.jpg"></image>
                <text>PPTV</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_7.jpg"></image>
                <text>小米</text>
              </navigator>
              <navigator url="/pages/list/index">
                <image src="http://static.botue.com/ugo/uploads/brand_8.jpg"></image>
                <text>长虹</text>
              </navigator>
            </view>
          </view> -->
        </scroll-view>
      </view>
    </view>
  </view>
</template>

<script>
import search from '@/components/search';

export default {
  data () {
    return {
      list: [],
      ac_index: 0
    }
  },
  components: {
    search
  },
  methods: {
    async getList () {
      const res = await this.request({
        url: '/api/public/v1/categories'
      })
      this.list = res.message
    },
    change (index) {
      this.ac_index = index
    }
  },
  onLoad () {
    this.getList()
  }
}
</script>

<style scoped lang="less">
scroll-view {
  height: 100%;
}

.category {
  display: flex;
  width: 100%;
  position: absolute;
  top: 100rpx;
  bottom: 0;

  .sup {
    width: 196rpx;
    background-color: #f4f4f4;

    text {
      display: block;
      height: 100rpx;
      text-align: center;
      line-height: 100rpx;
      font-size: 27rpx;
      color: #333;
      border-bottom: 1rpx solid #eee;

      &:last-child {
        border-bottom: none;
      }

      &.active {
        background-color: #fff;
        color: #ea4451;
        position: relative;

        &::before {
          content: "";
          display: block;
          width: 8rpx;
          height: 60rpx;
          transform: translateY(-50%);
          background-color: #ea4451;

          position: absolute;
          left: 0;
          top: 50%;
        }
      }
    }
  }

  .sub {
    flex: 1;
    padding: 20rpx 18rpx;

    .thumb {
      width: 100%;
      height: 180rpx;
    }

    .children {
      text-align: center;
      color: #333;

      .title {
        display: inline-block;
        margin: 40rpx 0 20rpx;
        font-size: 30rpx;

        &::before {
          content: "/";
          margin-right: 20rpx;
          color: #666;
        }

        &::after {
          content: "/";
          margin-left: 20rpx;
          color: #666;
        }
      }
    }

    .brands {
      display: flex;
      flex-wrap: wrap;

      navigator {
        width: 33%;
        margin-bottom: 20rpx;
      }

      image {
        width: 120rpx;
        height: 120rpx;
      }

      text {
        display: block;
        font-size: 24rpx;
      }
    }
  }
}
</style>
