<template>
    <div class="working-horse-wrapper">
        <div class="working-horse-row ">
            <div class="working-horse-title working-horse-title-settings">
                Schedule
            </div>
            <div class="working-horse-content working-horse-content-settings">
                <span style="padding-right: 10px;" class="flex-center">
                    <div class="radio-wrapper">
                        <label for="radioFixed" class="flex-center">
                            <input type="radio" name="typeRadio" checked id="radioFixed" class="radio-input">
                            <div class="radio-design"></div> Fixed
                        </label>
                    </div>
                </span>
                <span class="flex-center">
                    <div class="radio-wrapper">
                        <label for="radioFlexible" class="flex-center">
                            <input type="radio" name="typeRadio" id="radioFlexible" class="radio-input">
                            <div class="radio-design"></div>Flexible
                        </label>
                    </div>
                </span>
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
                <div class="checkbox-wrapper">
                    <input type="checkbox" v-model="item.check" :id="'check-'+key" class="checkbox-input">
                    <label class="checkbox-design" :for="'check-'+key">
                        <i class="fa fa-check" aria-hidden="true" v-if="item.check"></i>
                    </label>
                </div>
                {{item.name}}
            </div>
            <div class="working-horse-content">
                <div :style="{visibility: item.check ? 'visible' : 'hidden'}">
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
        color: #888;
    }
    .working-horse-content{
        flex-basis: 80%;
        adding-bottom: 20px;
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
    .checkbox-design{
        width: 20px;
        height: 20px;
        background-color: #54cc3e;
        border-radius: 3px;
        color: #fff;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-right: 5px;
        border: 2px solid #74ca68;
        box-sizing: border-box;
    }
    .checkbox-input,
    .radio-input{
        display: none;
    }
    .radio-design{
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 1px solid #ccc;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-right: 5px;
    }
    .radio-input:checked ~ .radio-design:after{
        display: block;
    }
    .radio-design:after{
        content:'';
        display: none;
        width: 14px;
        height: 14px;
        background-color: #448fe3;
        border-radius: 50%;
    }
    .flex-center{
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
