<template>
    <div class="count-container">
        <button type="button" class="sub" @click="sub">-</button>
        <input type="number" class="count" v-model.number.lazy="number"/>
        <button type="button" class="add" @click="add">+</button>
    </div>
</template>
<script>
export default {
    name: 'EsCount',
    emits:['countChange'],
    // props 的值是只读
    props:{
        num:{
            type:Number,
            default:0,
            required:true
        },
        min:{
            type:Number,
            default:NaN
        }
    },
    data(){
        return {
            number:this.num
        }
    },
    methods:{
        sub(){
            if(!isNaN(this.number)&& this.number -1 < this.min) return
            this.number--
        },
        add(){
            this.number++
        }
    },
    watch:{
        number(newVal){
            const parseResult = parseInt(newVal)
            if(isNaN(parseResult) || parseResult<1){
                this.number =1
                return
            }
            if(String(newVal).indexOf('.')!==-1){
                this.number = parseResult
                return
            }
            this.$emit('countChange',this.number)
        }
    }
}
</script>
<style scoped>
input {
    width: 25px;
    outline: none;
}

</style>