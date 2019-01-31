<template>
  <div class="search-panel">
    <el-row class="m-header-searchbar">
      <el-col
        :span="3"
        class="left">
        <img
          src="//s0.meituan.net/bs/fe-web-meituan/e5eeaef/img/logo.png"
          alt="美团">
      </el-col>
      <el-col
        :span="15"
        class="center">
        <div class="wrapper">
          <el-input v-model="search" placeholder="搜索商家和地点" 
            @focus="focus" 
            @blur="blur" 
            @input="input">
         </el-input>
          <button class="el-button el-button--primary"><i class="el-icon-search" /></button>
          <dl class="hotPlace"  v-if="isHotPlace">
            <dt>热门搜索</dt>
            <dd v-for="(item,idx) in hotPlace" :key="idx">{{item}}</dd>
          </dl>
          <dl class="searchList" v-if="isSearchList">
            <dd v-for="(item,idx) in searchList" :key="idx">{{item}}</dd>
          </dl>
        </div>
        <p class="suggest">
          <a href="#">11111111111</a>
          <a href="#">11111111111</a>
          <a href="#">11111111111</a>
        </p>
        <ul class="nav">
          <li>
            <nuxt-link
              to="/"
              class="takeout"
            >美团外卖</nuxt-link>
          </li>
          <li>
            <nuxt-link
              to="/"
              class="movie"
            >猫眼电影</nuxt-link>
          </li>
          <li>
            <nuxt-link
              to="/"
              class="hotel"
            >美团酒店</nuxt-link>
          </li>
          <li>
            <nuxt-link
              to="/"
              class="apartment"
            >民宿/公寓</nuxt-link>
          </li>
          <li>
            <nuxt-link
              to="/"
              class="business"
            >商家入驻</nuxt-link>
          </li>
        </ul>
      </el-col>
      <el-col
        :span="6"
        class="right">
       <!--  <ul class="security">
          <li><i class="refund"/><p class="txt">随时退</p></li>
          <li><i class="single"/><p class="txt">不满意免单</p></li>
          <li><i class="overdue"/><p class="txt">过期退</p></li>
        </ul> -->
      </el-col>
    </el-row>
  </div>
</template>


<script>
export default {
  data() {
    return {
      search: "", //input是否有值决定搜索下拉框是热门推荐 还是 搜索内容
      isFocus: false,
      hotPlace: ['火锅','火锅','火锅'],
      searchList: ['故宫','故宫','故宫']
    };
  },
  computed:{
    isHotPlace:function(){
      return this.isFocus&&!this.search //聚焦状态 && 值为空
    },
    isSearchList:function(){
      return this.isFocus&&this.search //聚焦状态 && 值不为空
    }
  },
  methods:{
      focus() {
          this.isFocus = true;
      },
      blur() {
         let self = this;
         //延时收起下拉框，因为不延时下拉直接消失点击下拉里边得文字就没效果了
         setTimeout(()=>{
            this.isFocus = false;
         },300)
      },
      input() {

      }
  }
};
</script>

