<template>
  <view class="content">
    <!--首页是功能帮助，目前提供九宫格模式与列表模式-->
    <view class="part">
      <uni-notice-bar single="true" scrollable :text="notice"/>
    </view>
<!--    <view class="part">
      <uni-segmented-control :values="['九宫格','折叠列表']" styleType="button" activeColor="#4F9BFA"></uni-segmented-control>
    </view>
    &lt;!&ndash;这里是九宫格模式部分的显示&ndash;&gt;
    <view class="part">
      <uni-grid :column="5">
        <uni-grid-item v-for="group in funcGroups">
          <text class="text">{{ group.group }}</text>
        </uni-grid-item>
      </uni-grid>
    </view>-->

    <view class="part">
      <uni-collapse v-for="group in groups" :open="true" accordion>
        <text class="text">{{ group.group }}</text>
        <uni-collapse-item class="funcDetailView" v-for="func in group.funcList" :title="func.functionName">
          <view>
            <text class="funcCmd">
              <text>指令: </text>
              <text class="at">@机器人</text>
              {{ func.functionCmd }}
            </text>
          </view>
          <view style="margin-top: 10px">
            <text class="desc">{{ func.functionDesc }}</text>
          </view>
          <view style="margin-top: 10px" v-if="func.isAdmin">
            <text class="admin">仅管理可用</text>
          </view>
        </uni-collapse-item>
      </uni-collapse>

    </view>

  </view>
</template>

<script setup lang="ts">
import {ref} from 'vue'
import {FunctionHelp} from "../../models/FunctionHelp";

const notice = ref('这里是一个通知。')

const groups: Array<{ group: string, icon?: string, funcList: Array<FunctionHelp> }> =
    [
      {
        group: "基础指令",
        funcList: [
          {
            functionName: "签到",
            functionCmd: "/签到",
            functionDesc: "每日签到获取积分"
          }, {
            functionName: "投喂",
            functionCmd: "/投喂猫猫",
            functionDesc: "使用100积分投喂猫猫，会增加好感度。"
          }, {
            functionName: "查询好感度",
            functionCmd: "/好感度",
            functionDesc: "查看自己的好感度。同时可以查看自己的积分。"
          }
        ]
      }, {
      group: "猫猫大作战",
      funcList: [
        {
          functionName: "😹丢猫猫",
          functionCmd: "/丢猫猫",
          functionDesc: "消耗100积分，在频道里丢出一只猫猫，猫猫会获得随机的词缀。"
        }, {
          functionName: "🐱捡猫猫",
          functionCmd: "/捡猫猫",
          functionDesc: "在频道里捡猫猫，会获得一只随机的别人丢出的猫猫。"
        }, {
          functionName: "🙀捡猫猫排行",
          functionCmd: "/捡猫猫排行",
          functionDesc: "查看频道内谁捡的猫猫最多，同时根据词缀得到分数。"
        }, {
          functionName: "🙀丢猫猫排行",
          functionCmd: "/丢猫猫排行",
          functionDesc: "查看频道内谁丢的猫猫最多，丢猫猫越多自己捡猫猫的分数也会又更多加成。"
        }
        , {
          functionName: "🧬清空频道内丢出的猫猫",
          functionCmd: "/偷走猫猫",
          functionDesc: "清空频道内丢出的猫猫，但是猫猫太可爱了，所以猫猫不会真的消失，只是你把猫猫都偷走了。",
          isAdmin:true
        }
      ]
    }
    ]
const funcGroups = ref(groups)
</script>

<style lang="scss">
.content {
  margin: 20rpx;
}

.part {
  margin-top: 20rpx;
}

.funcCmd {
  color: $uni-text-color;
  font-size: 30rpx;
}

.funcDetailView {
  margin: 10rpx;
}

.funcDetailView .at {
  color: $uni-color-primary;
}
.funcDetailView .desc {
  color: $uni-text-color-grey;

}
.funcDetailView .admin {
  color: $uni-color-warning;

}
.title {
  font-size: 36rpx;
  color: #333333;
}
</style>
