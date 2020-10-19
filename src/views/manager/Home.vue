<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
   <!-- 内容区域 -->
   <div>
     <!-- --{{categories}} -->
     <!-- 分类 6个 -->
      <van-grid :column-num="3">
        <van-grid-item
          v-for="value in categories"
          :key="value.id"
          :icon="value.icon"
          :text="value.name"
        />
      </van-grid>
     <!-- 产品 6个 -->
     <briup-product-item @click="toBuyHandler(p)" v-for="p in products" :key="p.id" :data="p">
     </briup-product-item>
   </div>
  </div>
</template>
<script>
import {get,post} from '../../http/axios';
export default {
  data(){
    return{
      categories:[],
      products:[]
    }
  },
  
  created(){
    //查询栏目信息
    this.loadCatagories();
    //查询产品信息
    this.laodProducts();
  },
  methods:{
    toBuyHandler(p){
      // alert(JSON.stringify(p));
      //跳转到订单确认页面，并且携带数据p
      this.$router.push({
        path:"/manager/order_confirm",
        query:p
      })
    },
    //加载栏目信息
    loadCatagories(){
    let url="/category/findAll";
    get(url).then((response)=>{
      //push foreach slice [1,2,3,4,5,6,7]
      //将
      this.categories=response.data.slice(0,6);
    })
    },

    //加载产品信息
    laodProducts(){
      let url="/product/query"
      let params={ page:0,pageSize:100 }
      post(url,params).then((response)=>{
        this.products = response.data.list;
      })
    }

  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>