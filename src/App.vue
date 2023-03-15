<template>
  <div class="app-container">
    <EsHeader title="购物车"></EsHeader>
    <es-goods v-for="item in goodsList"
    :key="item.id" :id="item.id" 
    :price="item.goods_price" 
    :count="item.goods_count"
    :check="item.goods_state" 
    :thumb="item.goods_img" 
    :title="item.goods_name"
    @stateChange="onGoodStateChage"
    @countChange="onCountChang"
    >
    </es-goods>
    <EsFooter @fullChange="onFullStateChange" :amount="amount" :total="total"></EsFooter>
  </div>
</template>

<script>
import EsHeader from './components/es-header/EsHeader.vue'
import EsFooter from './components/es-footer/EsFooter.vue'
import EsGoods from './components/es-goods/EsGoods.vue'

export default {
  name: 'App',
  data() {
    return {
      goodsList: [],
    }
  },

  created() {
    this.getGoodsList()
  },

  methods: {
    async getGoodsList() {
      const { data: res } = await this.$http.get('/api/cart')
      if (res.status !== 200) return
      this.goodsList = res.list
    },
    // 全选状态变化
    onFullStateChange(isFull) {                    
     this.goodsList.forEach(x=>x.goods_state= isFull)
    },
    //商品选中状态
    onGoodStateChage(e){
    const findResult = this.goodsList.find(x=> x.id === e.id)
      if(findResult){
        findResult.goods_state = e.value
      }
    },

    onCountChang(good){
      const findResult = this.goodsList.find(x=>x.id=good.id)
      if(findResult){
        findResult.goods_count = good.count
      }
    }

  },

  computed:{
    amount(){
      return this.goodsList.reduce((pre,cur)=>{
      if(cur.goods_state!==true) return pre
      else return pre + cur.goods_count*cur.goods_price
     },0)
  },

  total(){
    return this.goodsList.reduce((pre,cur)=>{
      if(cur.goods_state!==true) return pre
      else return pre + cur.goods_count
    },0)
  }
  },
  // 组件注册
  components: {
    EsHeader,
    EsFooter,
    EsGoods,
  }
}
</script>

<style scoped>

app-container {
  padding-bottom: 50px;
}

</style>