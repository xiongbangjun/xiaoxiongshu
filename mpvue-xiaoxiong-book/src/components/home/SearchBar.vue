<template>
    <div class="search-bar">
        <div class="search-bar-wrapper" @click="onSearchBarClick">
            <van-icon class="search" name="search" size="16px" color="#858C96"/>
            <input 
            class="search-bar-input"
            :focus="focus"
            :disabled="disabled"
            :maxlength="limit"
            :placeholder="hotSearch.length ===0 ? '搜索':hotSearch"
            v-model="searchWorld"
            @input="onChange"
            @confirm="onConfirm"
            placeholder-style="color: #ADB4BE;font-size: 15px"
            />
            
            <van-icon 
            class="clear" 
            name="clear" 
            size="16px" 
            color="#ccc"
            @click="onClearClick"
            confirm-type="search"
            v-if="searchWorld.length>0"
            />
        </div>
    </div>
</template>
<script>
export default {
    props:{
        focus:{
        type:Boolean,
        default:false
    },
    disabled:{
        type:Boolean,
        default:false
    },
    limit:{
        type:Number,
        default:50
    },
    hotSearch:{
        type:String,
        default:''
    }
    },
    data() {
        return {
            searchWorld:''
        }
    },
    methods:{
        onSearchBarClick(){
            this.$emit('onClick')
        },
        onClearClick(){
            this.searchWorld=''
            this.$emit('onClear')
        },
        onChange(e){
            const {value} = e.mp.detail
            this.$emit('onChange',value)
        },
        onConfirm(e){
            const {value} = e.mp.detail
            this.$emit('onConfirm',value) 
        },
        setValue(v){
            this.searchWorld=v
        },
        getValue(){
            return this.searchWorld
        }
    }
}
</script>
<style lang="scss" scoped>
    .search-bar{
        padding:15px 15.5px;
        .search-bar-wrapper{ 
            display: flex;
                align-items:center;
                box-sizing: border-box;
                height: 40px;
                background:#F5F5F9;
                border-radius:20px;
                padding:12px 17px;
            .search-bar-input{
                flex:1;
                margin:0 8px;
                color: #333;
                font-size: 15px;
            }
            .search,.clear{
                display: flex;
                align-items:center;
                height: 100%;
            }
            
        }
    }
</style>
