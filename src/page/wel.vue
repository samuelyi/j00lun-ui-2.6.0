<template>
  <div>
    <basic-container>
      <!--<iframe src="http:// " class="iframe-home"></iframe>-->

      <el-card class="box-card" style="margin-top: 20px">
        <div slot="header" class="clearfix">
          <span>实时概况</span>
        </div>
        <avue-data-icons :option="option2"></avue-data-icons>
      </el-card>
      <el-card class="box-card" style="margin-top: 20px">
        <div slot="header" class="clearfix">
          <span>活跃数量</span>
        </div>
        <avue-data-display :option="option3"></avue-data-display>
      </el-card>
      <el-alert
              title="本页面数据为随机模拟，并非真实数据，仅作展示"
              type="info"
              :closable="false"
              center
              show-icon>
      </el-alert>
    </basic-container>
  </div>
</template>

<script>
  import {mapGetters} from 'vuex';

  export default {
    name: 'wel',
    data() {
      return {
        option1: {
          data: [
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '商品总量',
              subtitle: '实时',
              count: 799,
              text: '当前商品总数量',
              color: 'rgb(27, 201, 142)',
              key: '商'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '用户总量',
              subtitle: '实时',
              count: 32112,
              text: '当前用户总数量',
              color: 'rgb(230, 71, 88)',
              key: '用'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '订单总量',
              subtitle: '实时',
              count: 908,
              text: '已付款订单总数量',
              color: 'rgb(178, 159, 255)',
              key: '订'
            }
          ]
        },
        option2: {
          span:6,
          data: [
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '今日注册',
              count: 12678,
              icon: 'el-icon-tickets',
              href:'http:// /',
              target:'_blank'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '今日登录',
              count: 22139,
              icon: 'el-icon-success',
              href:'http:// /',
              target:'_blank'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '今日订阅',
              count: 35623,
              icon: 'el-icon-info',
              href:'http:// /',
              target:'_blank'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              title: '今日评论',
              count: 16826,
              icon: 'el-icon-message',
              href:'http:// /',
              target:'_blank'
            }
          ]
        },
        option3: {
          span:6,
          data: [
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              count: 100,
              title: '日活跃数',
              href:'http:// /',
              target:'_blank'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              count: '3,000',
              title: '月活跃数',
              href:'http:// /',
              target:'_blank'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              count: '20,000',
              title: '年活跃数',
              href:'http:// /',
              target:'_blank'
            },
            {
              click: function (item) {
                // alert(JSON.stringify(item));
              },
              count: '40,000',
              title: '周活跃数',
              href:'http:// /',
              target:'_blank'
            }
          ]
        },
      }
    },
    computed: {
      ...mapGetters(['website'])
    },
    created() {

    },
    methods: {
    }
  }
</script>

<style scoped="scoped" lang="scss">
  .iframe-home {
    width: 100%;
    height: 800px;
    border: unset;
  }
</style>
