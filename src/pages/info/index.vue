<template>
  <view style="margin-top: 10px;width: 100%;display: flex;align-items:center;flex-direction: column;">

    <image style="width: 200rpx; height: 200rpx; background-color: #eeeeee;" mode="aspectFit"
           :src="avatar"></image>
    <text style="margin-top: 10px">{{ bot }}</text>
  </view>
  <uni-list>
    <uni-list-item title="关于"></uni-list-item>
    <uni-list-item title="Bot版本"
                   thumb="/static/version.png"
                   :rightText="version"></uni-list-item>
    <uni-list-item title="开发者"
                   thumb="/static/developer.png"
                   :rightText="developer"></uni-list-item>
    <uni-list-item title="开发者的话"
                   showArrow
                   thumb="/static/love.png"
                   clickable @click="onClick"></uni-list-item>
  </uni-list>
</template>

<script setup>
import {ref} from "vue";

const popup = ref(null)//防止setup用不了ref popup


//Bot名字
const bot = ref("猫猫不吃鱼")
//头像
const avatar = ref("https://tse2-mm.cn.bing.net/th/id/OIP-C.1KRa9cMmBQoMqyPBPz24hgHaHa?pid=ImgDet&rs=1");
//开发者的话
const msgToSay = ref("你好，我想对你说，赫尔没有对象。（怨");
//Bot版本
const version = ref("1.0.0");
//开发者
const developer = ref("赫尔没有中二病");

//一个方法，无需在意。
const onClick = () => {
  uni.showModal({
    title: '开发者的话',
    content: msgToSay,
  });
}

</script>

<style scoped>

</style>
