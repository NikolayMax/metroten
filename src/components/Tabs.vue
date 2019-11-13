<template>
    <div class="tabs-wrapper">
        <div class="tabs-header">
            <div class="tabs-header-item"
                 v-for="(item, key) in tabs"
                 v-on:click="onSelect(item)"
                 v-bind:class="{'tabs-header-item-selected': item.selected}"
                 :key="key">{{item.label}}</div>
        </div>
        <div class="tabs-body" v-if="typeof tabs.find(item=>item.selected).content !== 'string'" v-bind:is="tabs.find(item=>item.selected).content"></div>
        <div class="tabs-body" v-else-if="typeof tabs.find(item=>item.selected).content === 'string'">
            {{tabs.find(item=>item.selected).content}}
        </div>
    </div>
</template>

<script>
    export default {
        name: "Tabs",
        props:['items'],
        data:(props)=>({
            tabs:props.items
        }),
        methods:{
            onSelect(item){
                this.tabs.map(item=>{
                    item.selected=false;
                    return item;
                });
                item.selected=true;
            }
        }
    }
</script>

<style scoped>
    .tabs-wrapper{
        background-color: #fff;
        border-radius: 6px;
        box-shadow: 0px 0px 7px -6px #000;
    }
    .tabs-header{
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        border-bottom: 1px solid #ccc;
    }
    .tabs-header-item{
        padding: 10px 30px;
        color: #751011;
        font-size: 18px;
        cursor: pointer;
        font-family: 'Heebo-Medium';
    }
    .tabs-header-item-selected{
        border-bottom: 2px solid #751011;
        color: #000;
    }
</style>
