<template>
    <div class="footer-container">
        <!-- 全选区域 -->
        <div class="check-all-container">
            <input type="checkbox" id="checkAll" :checked="isFull" @change="fullChange" />
            <label for="checkAll">全选</label>
        </div>

        <!-- 合计区域 -->
        <div>
            <span>合计：</span>
            <span class="amount">￥{{ amount.toFixed(2) }}</span>
        </div>

        <button type="button" class="pay" :disabled="total === 0">结算 {{ total }}</button>

    </div>
</template>
<script>
export default {
    name: 'EsFooter',
    emits: ['fullChange'],
    props: {
        // 已勾选的商品总价
        amount: {
            type: Number,
            default: 0
        },
        // 已勾选的商品总数
        total: {
            type: Number,
            default: 0
        },
        isFull: {
            type: Boolean,
            default: false
        }
    },

    methods: {
        fullChange(e) {
            this.$emit('fullChange', e.target.checked)
        }

    }

}
</script>
<style scoped>
.footer-container {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 50px;
    border-top: 1px solid #efefef;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 10px;
    background-color: white;
}

.check-all-container {
    display: flex;
    align-items: center;
}

.amount {
    font-weight: bold;
    color: red;
}

.pay {
    color: white;
    background-color: #047bfe;
    border-radius: 20px;
    border: none;
    font-size: 12px;
    padding: 5px 15px;
    margin-right: 30px;
}
</style>