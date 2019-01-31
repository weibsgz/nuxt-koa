<template>
  <div class="m-menu">
    <dl class="nav" @mouseleave="mouseleave">
      <dt>全部分类</dt>
      <dd v-for="(item,idx) in menu" :key="idx" @mouseenter="enter">
        <i :class="item.type"></i>{{item.name}}<span class="arrow" />
      </dd>
    </dl>
    <div class="detail" v-if="kind" @mouseenter="sover" @mouseleave="sout">
       <template v-for="(item,idx) in curdetail.child" >
          <h4>{{item.title}}</h4>
          <span v-for="(v,idx1) in item.child"  :key="idx1">{{v}}</span>
       </template>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      kind:'', //鼠标HOVER时候区分是哪个选项
      menu: [
        {
          type: "food",
          name: "美食",
          child: [
            {
              title: "美食",
              child: ["代金券", "甜点饮品", "火锅", "自助餐", "小吃快餐"]
            }
          ]
        },
        {
          type: "takeout",
          name: "外卖",
          child: [
            {
              title: "外卖",
              child: ["美团外卖"]
            }
          ]
        },
        {
          type: "hotel",
          name: "酒店",
          child: [
            {
              title: "酒店星级",
              child: ["经济型", "舒适/三星", "高档/四星", "豪华/五星"]
            }
          ]
        }
      ]
    };
  },
  computed:{
    curdetail() {
    
      //filter 返回一个新数组 箭头函数不加括号 代表默认return
      return this.menu.filter((v)=>
        v.type == this.kind
      )[0]
    }
  },
  methods:{
    mouseleave() {
      let self = this;
      this.timer = setTimeout(()=>{
        self.kind = ''
      },200)
      
    },
    enter(e) {
       
      this.kind = e.target.querySelector('i').className;
      console.log(JSON.stringify(this.curdetail))
    },
    sover() { //滑到子菜单不能消失
     clearTimeout(this.timer)
    },
    sout() {
      this.kind = ''
    }
  }
};
</script>

<style lang="scss">
  .m-menu {
    margin-top:110px!important;
  }
</style>
