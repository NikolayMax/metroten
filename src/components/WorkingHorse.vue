<template>
    <div class="working-horse-wrapper">
        <div class="working-horse-row ">
            <div class="working-horse-title working-horse-title-settings">
                Schedule
            </div>
            <div class="working-horse-content working-horse-content-settings">
                <span style="padding-right: 10px;"><input type="radio" name="typeRadio" checked> Fixed</span>
                <span><input type="radio" name="typeRadio"> Flexible</span>
            </div>
        </div>
        <div class="working-horse-row">
            <div class="working-horse-title">
                Working hourse
            </div>
            <div class="working-horse-content">
                <Slider />
            </div>
        </div>
        <div class="working-horse-row" v-for="(item, key) in items" :key="key">
            <div class="working-horse-title">
                <input type="checkbox" v-model="item.check">
                {{item.name}}
            </div>
            <div class="working-horse-content">
                <div v-if="item.check">
                    <Slider />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Slider from './Slider';

    export default {
        name: "WorkingHorse",
        components:{
            Slider
        },
        data:()=>({
            items:[
                {name:'Monday',check:true},
                {name:'Tuesday',check:true},
                {name:'Wedndesday',check:true},
                {name:'Thursday',check:true},
                {name:'Friday',check:true},
                {name:'Saturday',check:false},
                {name:'Sunday',check:false},
            ]
        })
    }
</script>

<style scoped>
    .working-horse-wrapper{
        padding: 20px;
    }
    .working-horse-row{
        display: flex;
        margin-bottom: 10px;
    }
    .working-horse-title{
        flex-basis: 20%;
        display: flex;
        align-items: center;
    }
    .working-horse-content{
        flex-basis: 80%;
    }
    .working-horse-title-settings{
        border-bottom: 1px solid #ccc;
        padding-bottom: 10px;
    }
    .working-horse-content-settings{
        justify-content: flex-start;
        display: flex;
        border-bottom: 1px solid #ccc;
        padding-bottom: 10px;
    }
</style>
