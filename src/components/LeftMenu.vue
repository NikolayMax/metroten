<template>
    <div class="left-menu">
        <div class="left-menu-links">
            <div class="left-menu-link" v-for="(item, key) in items" v-bind:key="key">
                <span class="left-menu-link-icon">
                    <i class="fa" v-bind:class="{[item.icon]:true}" aria-hidden="true"></i>
                </span>
                <span class="left-menu-link-name">{{item.name}}</span>
            </div>
        </div>
        <div class="left-menu-user">
            <div class="left-menu-user-icon">
                <img src="https://brod.kz/media/persons/szuawc/1538393783g3l8y.jpg" alt="">
            </div>
            <div class="left-menu-user-name">Settings</div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "LeftMenu",
        data:()=>({
            items:[
                {id:1,name:'Dashboard', icon:'fa-tachometer'},
                {id:2,name:'Customers', icon:'fa-user'},
                {id:3,name:'Calendar', icon:'fa-calendar'},
                {id:4,name:'Chats', icon:'fa-comments-o'},
                {id:5,name:'Tasks', icon:'fa-tasks'},
                {id:6,name:'Inbox', icon:'fa-inbox'},
                {id:7,name:'Calls', icon:'fa-phone'},
                {id:8,name:'Leads', icon:'fa-leanpub'},
                {id:9,name:'Team', icon:' fa-users'},
            ]
        })
    }
</script>

<style scoped>
    .left-menu{
        width: 250px;
        background-color: #e91c20;
        color: #ffffff;
        padding-top: 80px;
        position: fixed;
        left: 0px;
        bottom: 0px;
        top: 0px;
    }
    .left-menu-link{
        padding: 10px 20px;
        text-align: left;
        cursor: pointer;
    }
    .left-menu-link-icon{
        font-size: 25px;
        margin-right: 15px;
    }
    .left-menu-link-name,
    .left-menu-user-name{
        font-size: 18px;
        font-weight: bold;
    }
    .left-menu-user{
        padding: 10px 20px;
        background-color: rgba(0,0,0,0.5);
    }
    .left-menu-user{
        position: absolute;
        bottom: 0px;
        width: 100%;
        box-sizing: border-box;
        display: flex;
        align-items: center;
    }
    .left-menu-user-icon{
        width: 40px;
        height: 40px;
        border-radius: 50%;
        border: 3px solid rgba(255, 255, 255, 0.6);
        overflow: hidden;
        margin-right: 15px;
    }
    .left-menu-user-icon img{
        width: 100%;
    }
</style>
