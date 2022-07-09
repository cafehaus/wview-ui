<template>
  <!-- 左图列表 -->
  <view class="left-img" v-if="type ? type === 1 : articleStyle === 1">
    <block v-for="(item, index) in list">
      <!-- 系统广告 -->
      <view
        :key="index"
        class="left-img-ad"
        v-if="{{index % item.listAdEvery === 0  && index && item.listAd =='1'  && showAd}}"
      >
        <block v-if="item.listAdtype === 'banner'">
          <ad
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'video'">
          <ad
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'grid'">
          <ad
            :unit-id="item.gridAdId"
            ad-type="grid"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'banner,video'">
          <ad
            v-if="(index / item.listAdEvery) % 2 === 0"
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
          <ad
            v-else
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
      </view>

      <!-- 文章列表 -->
      <view
        :key="index"
        class="left-img-item"
        @click="goto(item)"
      >
        <image
          show-menu-by-longpress
          :src="item.img || item.postcover || item.post_medium_image"
          mode="aspectFill"
          :class="[item.format === 'video' ? 'img-cover-video left-img-cover' : 'left-img-cover']"
        />

        <view class="left-img-content">
          <view class="left-img-title">
            <text class="txt">{{ item.title.rendered }}</text>
          </view>

          <view class="left-img-des">
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt">付费阅读 {{ item.payForCount }}</text>
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
        </view>
      </view>
    </block>
  </view>

  <!-- 右图列表 -->
  <view
    class="right-img"
    v-else-if="type ? type === 2 : articleStyle === 2"
  >
    <block v-for="(item, index) in list">
      <!-- 广告 -->
      <view
        :key="index"
        class="right-img-ad"
        v-if="index % item.listAdEvery === 0 && index && item.listAd === '1' && showAd"
      >
        <block v-if="item.listAdtype === 'banner'">
          <ad
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'video'">
          <ad
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'grid'">
          <ad
            :unit-id="item.gridAdId"
            ad-type="grid"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'banner,video'">
          <ad
            v-if="(index / item.listAdEvery) % 2 === 0"
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
          <ad
            v-else
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
      </view>

      <!-- 文章 -->
      <view
        :key="index"
        class="right-img-item"
        @click="goto(item)"
      >
        <view class="right-img-content">
          <view class="right-img-title">
            <text class="txt">{{ item.title.rendered }}</text>
          </view>

          <view class="right-img-des">
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt">付费阅读 {{ item.payForCount }}</text>
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
        </view>
        <image
          show-menu-by-longpress
          :src="item.img || item.postcover || item.post_medium_image"
          mode="aspectFill"
          :class="[item.format === 'video' ? 'img-cover-video right-img-cover' : 'right-img-cover']"
        />
      </view>
    </block>
  </view>

  <!-- 大图列表 -->
  <view class="big-img" v-else-if="type ? type === 3 : articleStyle === 3">
    <block v-for="(item, index) in list">
      <view
        :key="index"
        class="big-img-ad"
        v-if="index % item.listAdEvery === 0  && index && item.listAd === '1' && showAd"
      >
        <block v-if="item.listAdtype === 'banner'">
          <ad
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'video'">
          <ad
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'grid'">
          <ad
            :unit-id="item.gridAdId"
            ad-type="grid"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'banner,video'">
          <ad
            v-if="(index / item.listAdEvery) % 2 === 0"
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
          <ad
            v-else
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
      </view>

      <view
        :key="index"
        class="big-img-item"
        @click="goto(item)"
      >
        <image
          show-menu-by-longpress
          :src="item.img || item.postcover || item.post_large_image"
          mode="aspectFill"
          :class="[item.format === 'video' ? 'img-cover-video big-img-cover' : 'big-img-cover']"
        />
        <view class="big-img-title">
          <text class="txt">{{ item.title.rendered }}</text>
        </view>

        <view class="big-img-info">
          <view class="big-img-des">
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt">付费阅读 {{ item.payForCount }}</text>
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
          <text>{{ item.post_date }}</text>
        </view>
      </view>
    </block>
  </view>

  <!-- 多图列表 -->
  <view class="multi" v-else-if="type ? type === 4 : articleStyle === 4">
    <block v-for="(item, index) in list">
      <!-- 广告 -->
      <view
        :key="index"
        class="multi-ad"
        v-if="index % item.listAdEvery === 0  && index && item.listAd === '1' && showAd"
      >
        <block v-if="item.listAdtype === 'banner'">
          <ad
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'video'">
          <ad
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'grid'">
          <ad
            :unit-id="item.gridAdId"
            ad-type="grid"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'banner,video'">
          <ad
            v-if="(index / item.listAdEvery) % 2 === 0"
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
          <ad
            v-else
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
      </view>

      <!-- 一张大图列表（序号index是5的倍数时为大图模式）-->
      <view
        :key="index"
        v-if="index % 10 === 5"
        class="multi-bigone"
        @click="goto(item)"
      >
        <view class="multi-bigone-title">
          <text class="txt">{{ item.title.rendered }}</text>
        </view>
        <image
          :src="item.img || item.postcover || item.post_medium_image"
          mode="aspectFill"
          show-menu-by-longpress
          :class="[item.format === 'video' ? 'img-cover-video multi-bigone-cover' : 'multi-bigone-cover']"
        />
        <view class="multi-bigone-des">
          <view>
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt">付费阅读 {{ item.payForCount }}</text>
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
          <text>{{ item.post_date }}</text>
        </view>
      </view>

      <!-- 三张图片列表 -->
      <view
        :key="index"
        v-else-if="item.post_all_images.length > 2 && item.format !== 'video'"
        class="multi-three"
        @click="goto(item)"
      >
        <view class="multi-three-title">
          <text>{{ item.title.rendered }}</text>
        </view>
        <view class="multi-three-imgbox">
          <image
            show-menu-by-longpress
            class="img"
            :src="item.post_all_images[0].imagesurl"
            mode="aspectFill"
          />
          <image
            show-menu-by-longpress
            class="img"
            :src="item.post_all_images[1].imagesurl"
            mode="aspectFill"
          />
          <image
            show-menu-by-longpress
            class="img"
            :src="item.post_all_images[2].imagesurl"
            mode="aspectFill"
          />
        </view>
        <view class="multi-three-des">
          <view>
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt">付费阅读 {{ item.payForCount }}</text>
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
          <text>{{ item.post_date }}</text>
        </view>
      </view>

      <!-- 单张图片列表 -->
      <view
        :key="index"
        v-else
        class="multi-one"
        @click="goto(item)"
      >
        <view class="multi-one-content">
          <view class="multi-one-title">
            <text class="txt">{{ item.title.rendered }}</text>
          </view>
          <view class="multi-one-des">
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt"
                >付费阅读 {{ item.payForCount }}</text
              >
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
        </view>
        <image
          show-menu-by-longpress
          :src="item.img || item.post_medium_image"
          mode="aspectFill"
          :class="[item.format === 'video' ? 'img-cover-video multi-one-cover' : 'multi-one-cover']"
        />
      </view>
    </block>
  </view>

  <!-- 瀑布流 -->
  <view class="water" v-else-if="type ? type === 5 : articleStyle === 5">
    <view class="water-left">
      <block v-for="(item, index) in list">
        <view
          :key="index"
          v-if="index % 2 === 0"
          class="water-item"
          @click="goto(item)"
        >
          <image
            show-menu-by-longpress
            :src="item.img || item.postcover || item.post_medium_image"
            class="water-cover"
            mode="aspectFill"
            :class="[item.format === 'video' ? 'img-cover-video water-cover' : 'water-cover']"
          />
          <view class="water-content">
            <view class="water-title">
              <text>{{ item.title.rendered }}</text>
            </view>
            <view class="water-des">{{ item.category_name }} · {{ item.post_date }}</view>
          </view>
        </view>
      </block>
    </view>

    <view class="water-right">
      <block v-for="(item, index) in list">
        <view
          :key="index"
          v-if="index % 2 === 1"
          class="water-item"
          @click="goto(item)"
        >
          <image
            show-menu-by-longpress
            :src="item.img || item.postcover || item.post_medium_image"
            mode="aspectFill"
            :class="[item.format === 'video' ? 'img-cover-video water-cover' : 'water-cover']"
          />
          <view class="water-content">
            <view class="water-title">
              <text>{{ item.title.rendered }}</text>
            </view>
            <view class="water-des">{{ item.category_name }} · {{ item.post_date }}</view>
          </view>
        </view>
      </block>
    </view>
  </view>

  <!-- 无图列表 -->
  <view class="noimg" v-else-if="type ? type === 6 : articleStyle === 6">
    <block v-for="(item, index) in list">
      <view
        class="noimg-ad"
        index="{{index}}"
        v-if="index % item.listAdEvery === 0  && index && item.listAd === '1' && showAd"
      >
        <block v-if="item.listAdtype === 'banner'">
          <ad
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'video'">
          <ad
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'grid'">
          <ad
            :unit-id="item.gridAdId"
            ad-type="grid"
            ad-theme="white"
            @error="onError"
          />
        </block>
        <block v-else-if="item.listAdtype === 'banner,video'">
          <ad
            v-if="(index / item.listAdEvery) % 2 === 0"
            :unit-id="item.videoAdId"
            ad-type="video"
            ad-theme="white"
            @error="onError"
          />
          <ad
            v-else
            :unit-id="item.bannerAdId"
            ad-intervals="30"
            @error="onError"
          />
        </block>
      </view>

      <view
        :key="index"
        class="noimg-item"
        @click="goto(item)"
      >
        <view class="noimg-title">
          <text class="txt">{{ item.title.rendered }}</text>
        </view>

        <view class="noimg-excerpt">
          <rich-text nodes="{{item.excerpt.rendered}}"></rich-text>
        </view>

        <view class="noimg-des">
          <view>
            <block v-if="item.integralForCount || item.payForCount">
              <text class="txt">积分阅读 {{ item.integralForCount }}</text>
              <text v-if="system && system !== 'iOS'" class="txt">付费阅读 {{ item.payForCount }}</text>
            </block>
            <block v-else>
              <text class="txt">浏览 {{ item.pageviews }}</text>
              <text class="txt">评论 {{ item.total_comments }}</text>
              <text class="txt">点赞 {{ item.like_count }}</text>
            </block>
          </view>
          <text>{{ item.post_date }}</text>
        </view>

        <!-- 操作按钮 -->
        <view class="btn-box" v-if="showAction">
          <button
            class="btn"
            type="primary"
            size="mini"
            @click="submitPage(item)"
          >提交页面搜索({{ item.searhDataPostCount }})</button>

          <button
            class="btn"
            type="primary"
            size="mini"
            @click="submitContent(item)"
            >提交内容搜索({{ item.searhContentPostCount }})</button>

          <button
            class="btn"
            type="primary"
            size="mini"
            @click="sendSubscribeMessage(item)"
            >更新提醒</button
          >

          <button
            class="btn"
            size="small"
            @click="deleteTopic(item)"
          >删除</button>
        </view>
      </view>
    </block>
  </view>
</template>
<script>
export default {
  props: {
    list: Array,
    // 1 左图 2 右图 3 大图 4 多图 5 瀑布流 6 无图
    type: {
      type: Number,
      value: null
    },

    system: {
      type: String,
      value: null
    },

    showAction: {
      type: Boolean,
      value: false
    },
    isWppage: { // wp页面
      type: Boolean,
      value: false
    }
  },
  data() {
    return {
      showAd: true,
      articleStyle: config.articleStyle || 1
    }
  },
  attached: function () {
    console.log(this.data.type);
    if (!this.data.type) {
      let articleStyle = wx.getStorageSync('articleStyle') || config.articleStyle || 1
      console.log(this.data.articleStyle);
      this.setData({ articleStyle: Number(articleStyle) })
    }
  },
  methods: {
    // 跳转
    goto(e) {
      // wp页面跳转
      if (this.data.isWppage) {
        this.triggerEvent('click', e)
        return
      }

      let { id } = e.currentTarget
      let type = e.currentTarget.dataset.posttype || 'post'
      let format = e.currentTarget.dataset.format || ''
      let url = ''
      let channelsFeedId = e.currentTarget.dataset.channelsfeedid || ''
      let channelsId = e.currentTarget.dataset.channelsid || ''
      let mpPostLink = e.currentTarget.dataset.mppostlink || ''
      if (channelsFeedId) {
        if ((type == "post" && format == 'video') || type == "topic") {

          wx.openChannelsActivity({
            finderUserName: channelsId,
            feedId: channelsFeedId,
            success(res) {
              let params = {
                id: id
              }
              app.$api.updatePageviews(params).then(res => {
                console.log(res);
              })
            }
          })

          return;
        }

      }
      else if (mpPostLink) {
        if ((type == "post" && format == 'link') || type == "topic") {
          let url = "/pages/webview/webview?url=" + mpPostLink;
          wx.navigateTo({
            url:url,
            success(res)
            {
              let params = {
                id: id
              }
              app.$api.updatePageviews(params).then(res => {
                console.log(res);
              })
            }
          })

          return;
        }
      }
      if (type === 'post') {
        url = `../detail/detail?format=${format}&id=${id}`
      } else if (type === 'topic' || type === 'reply') {
        url = '../socialdetail/socialdetail?id=' + id
      }

      wx.navigateTo({
        url
      })
    },

    // 广告错误
    onError(e) {
      if (e.detail.errCode) {
        this.setData({
          showAd: false
        })
      }
    },

    submitPage(e) {
      this.triggerEvent('submitPage', e)
    },
    submitContent(e) {
      this.triggerEvent('submitContent', e)
    },

    deleteTopic(e) {
      this.triggerEvent('deleteTopic', e)
    },

    // 发送订阅消息
    sendSubscribeMessage(e) {
      this.triggerEvent('sendSubscribeMessage', e)
    }
  }
}
</script>
<style scoped>
/* 左图模式 */
.left-img {
  background: #f5f7f7;
}

.left-img-ad {
  margin-bottom: 16rpx;
}

.left-img-item {
  position: relative;
  padding: 40rpx;
  overflow: hidden;
  background-color: #fff;
  margin-bottom: 16rpx;
}

.left-img-cover {
  position: absolute;
  left: 40rpx;
  top: 40rpx;
  width: 240rpx;
  height: 180rpx;
  background: #f5f7f7;
}

.img-cover-video:after {
  content: '\e666';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: 'iconfont' !important;
  font-weight: normal;
  font-size: 64rpx;
  color: #fff;
}

.left-img-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 180rpx;
  margin-left: 270rpx;
}

.left-img-title {
  margin-bottom: 20rpx;
}

.left-img-title .txt {
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  font-size: 30rpx;
  line-height: 1.4;
  font-weight: 500;
  color: #333;
}

.left-img-des {
  margin-right: 40rpx;
  color: #959595;
  font-size: 24rpx;
}

.left-img-des .txt:not(:last-child) {
  margin-right: 32rpx;
}

/* 右图列表 */
.right-img {
  margin-bottom: 24rpx;
  background: #f5f7f7;
}

.right-img-ad {
  margin-bottom: 16rpx;
}

.right-img-item {
  position: relative;
  padding: 40rpx;
  min-height: 180rpx;
  overflow: hidden;
  background-color: #fff;
  margin-bottom: 16rpx;
}

.right-img-cover {
  position: absolute;
  right: 40rpx;
  top: 40rpx;
  width: 240rpx;
  height: 180rpx;
}

.right-img-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 180rpx;
}

.right-img-title {
  margin-bottom: 20rpx;
  width: 60%;
}

.right-img-title .txt {
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  font-size: 30rpx;
  line-height: 1.4;
  font-weight: 500;
  color: #333;
}

.right-img-des {
  width: 60%;
}

.right-img-des .txt {
  color: #959595;
  font-size: 24rpx;
}

.right-img-des .txt:not(:last-child) {
  margin-right: 32rpx;
}

/* 大图列表 */
.big-img {
  background: #f5f7f7;
}

.big-img-ad {
  margin-bottom: 16rpx;
}

.big-img-item {
  position: relative;
  overflow: hidden;
  background: #fff;
  padding: 40rpx;
  margin-bottom: 16rpx;
}

.big-img-cover {
  display: block;
  width: 100%;
  height: 360rpx;
  background: #f5f7f7;
  position: relative;
}

.big-img-cover:after {
  font-size: 88rpx;
}

.big-img-title {
  font-size: 32rpx;
  line-height: 1.6;
  font-weight: 500;
  color: #333;
  word-wrap: break-word;
  word-break: normal;
  margin-top: 16rpx;
}

.big-img-info {
  display: flex;
  justify-content: space-between;
  font-size: 24rpx;
  color: #959595;
  margin-top: 12rpx;
}

.big-img-des .txt:not(:last-child) {
  margin-right: 32rpx;
}

/* 多图模式 */
.multi {
  background: #f5f7f7;
}

.multi-ad {
  margin-bottom: 16rpx;
}
/* 一张大图 */
.multi-bigone {
  background: #fff;
  padding: 40rpx;
  margin-bottom: 16rpx;
}

.multi-bigone-cover {
  width: 100%;
  height: 360rpx;
  display: block;
  margin: 16rpx 0;
  background: #f5f7f7;
  position: relative;
}

.multi-bigone-cover:after {
  font-size: 88rpx;
}

.multi-bigone-title .txt {
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  font-size: 32rpx;
  line-height: 1.5;
  font-weight: 500;
  color: #333;
}

.multi-bigone-des {
  display: flex;
  justify-content: space-between;
  color: #959595;
  font-size: 24rpx;
}

.multi-bigone-des .txt {
  margin-right: 32rpx;
}
/* 三张图 */
.multi-three {
  padding: 40rpx;
  background: #fff;
  margin-bottom: 16rpx;
}

.multi-three-title {
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  font-size: 32rpx;
  line-height: 1.5;
  font-weight: 500;
  color: #333;
}

.multi-three-imgbox {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-column-gap: 8rpx;
  height: 180rpx;
  margin: 16rpx 0;
}

.multi-three-imgbox .img {
  width: 100%;
  height: 180rpx;
}

.multi-three-des {
  display: flex;
  justify-content: space-between;
  color: #959595;
  font-size: 24rpx;
}

.multi-three-des .txt {
  margin-right: 32rpx;
}
/* 一张小图 */
.multi-one {
  display: flex;
  padding: 40rpx;
  background: #fff;
  margin-bottom: 16rpx;
}

.multi-one-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 32rpx;
}

.multi-one-title .txt {
  text-overflow: -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  font-size: 32rpx;
  line-height: 1.5;
  font-weight: 500;
  color: #333;
}

.multi-one-des {
  color: #959595;
  font-size: 24rpx;
}

.multi-one-des .txt {
  margin-right: 32rpx;
}

.multi-one-cover {
  flex-shrink: 0;
  width: 218rpx;
  height: 180rpx;
  background: #f5f7f7;
  position: relative;
}

/* 瀑布流 */
.water {
  display: flex;
  padding: 8rpx;
}

.water-left,
.water-right {
  flex: 1;
}

.water-item {
  margin: 8rpx 8rpx 16rpx 8rpx;
  box-shadow: 0px 8rpx 20rpx 0px rgba(9, 36, 66, 0.2);
  border-radius: 8rpx;
  background: #fff;
  overflow: hidden;
}

.water-cover {
  width: 100%;
  height: 400rpx;
  display: block;
  position: relative;
}

.water-cover:after {
  font-size: 80rpx;
}

.water-content {
  padding: 20rpx 20rpx 30rpx;
  box-sizing: border-box;
}

.water-title {
  font-size: 15px;
  line-height: 1.4;
  color: #333;
  text-align: justify;
}

.water-des {
  font-size: 14px;
  color: #959595;
  margin-top: 6rpx;
}

/* 无图列表 */
.noimg {
  background: #f5f7f7;
}

.noimg-ad {
  margin-bottom: 16rpx;
}

.noimg-item {
  position: relative;
  overflow: hidden;
  background: #fff;
  padding: 40rpx;
  margin-bottom: 16rpx;
}

.noimg-cover {
  display: block;
  width: 100%;
  height: 360rpx;
  background: #f5f7f7;
}

.noimg-title {
  font-size: 32rpx;
  line-height: 1.6;
  font-weight: 500;
  color: #333;
  word-wrap: break-word;
  word-break: normal;
}

.noimg-excerpt {
  font-size: 28rpx;
  line-height: 1.6;
  color: #999;
  word-wrap: break-word;
  word-break: break-all;
  text-align: justify;
  padding-top: 10rpx;
}

.noimg-des {
  display: flex;
  justify-content: space-between;
  font-size: 24rpx;
  color: #999;
  margin-top: 20rpx;
}

.noimg-des .txt {
  margin-right: 32rpx;
}

.btn-box {
  padding-top: 20rpx;
  margin-top: 20rpx;
  border-top: 1px solid #eee;
}

.btn-box .btn {
  margin-right: 10rpx;
}
</style>