<template>
    <div class="router-wrapper">
        <h1 class="router-title">Settings</h1>
        <Tabs
            :items="tabs"
        />
        <div class="flex">
            <button class="button">Save changes</button>
            <a href="#" class="link-calcel">Cancel</a>
            <span>to reset chages</span>
        </div>
    </div>
</template>

<script>
    import Tabs from './Tabs.vue';
    import WorkingHorse from './WorkingHorse.vue';

    export default {
        components:{
            Tabs
        },
        name: "Router",
        data:()=>({
            tabs:[
                {
                    label:'Profile',
                    content:'Profile',
                    selected:false,
                },
                {
                    label:'Notifications',
                    content:'Notifications',
                    selected:false,
                },
                {
                    label:'Password',
                    content:'Password',
                    selected:false,
                },
                {
                    label:'Working horse',
                    content: WorkingHorse,
                    selected:true,
                },
                {
                    label:'Call Settings',
                    content:'Call Settings',
                    selected:false,
                },
            ]
        })
    }
</script>

<style scoped>
    .router-wrapper{
        margin-left: 250px;
        padding: 0px 20px 0px 80px;
    }
    .router-title{
        text-align: left;
        font-family: 'Heebo-Thin';
    }
    .flex{
        display: flex;
        align-items: center;
        background-color: #ececec;
        padding: 10px;
    }
    .flex > * { margin: 0 10px; }
    .button{
        background-color: #21d465;
        padding: 10px;
        text-transform: uppercase;
        border-radius: 5px;
        color: #fff;
        font-size: 14px;
        font-family: 'Heebo-Bold';
        border: 0px;
        cursor: pointer;
    }
    .button:focus{
        outline: none;
    }
    .link-calcel{
        color: #a42520;
        font-family: 'Heebo-Medium';
        text-decoration: none;
    }
    .link-calcel:hover{
        text-decoration: underline;
    }
</style>
