<template>
    <div class="goods-container">
        <div class="left">
            <input type="checkbox" :id="id" :checked="check" @change="onChange"/>
            <label :for="id">
                <!-- 商品缩略图 -->
                <img :src="thumb" alt="商品图片" class="thumb">
            </label>
        </div>

        <div class="right">
            <div class="top">{{ title }}</div>
            <div class="bottom">
                <div class="price">￥{{ price.toFixed(2) }}</div>
                <div class="count"><es-count :num = "count" :min="1" @countChange="onCountChange"></es-count></div>
            </div>

        </div>
    </div>
</template>
<script>

import EsCount from '../es-count/EsCount.vue'

export default {
    name: 'EsGoods',
    components:{
        EsCount,
    },
    emits:['stateChange','countChange'],
    props: {
        id: {
            type: [String, Number],
            required: true
        },
        // 缩略图
        thumb: {
            type: String,
            required: true
        },
        title: {
            type: String,
            required: true
        },
        price: {
            type: Number,
            required: true
        },
        // 数量
        count: {
            type: Number,
            required: true
        },
        // 是否勾选
        check: {
            type: Boolean,
            required: true
        },
    },
    methods:{
        onChange(e){
           this.$emit('stateChange', {
            id:this.id,
            value:e.target.checked
           })
        },
        // 数量值变化
        onCountChange(num){
          this.$emit('countChange',{
            id:this.id,
            count:num
          })
        }
    }
}
</script>
<style scoped>
.goods-container {
    display: flex;
}

.right {
    position: relative;
}

.left {
    flex: 1;
    display: flex;
    height: 100px;
}

.right {
    flex: 3;
    margin-left: 5px;
}

.thumb {
    background-color: #efefef;
    width:100px;
}

.price {
    position: absolute;
    left: 0;
    bottom: 0;
    color: red;
}

.count {
    position: absolute;
    right: 0;
    bottom: 0;
}
.top {
    text-align: left;
    font-weight: bold;
    font-size: 10px;
}

.goods-container {
    border-top: 1px solid #e4e4e4;

    padding: 15px;
}
</style>