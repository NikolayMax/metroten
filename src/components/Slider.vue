<template>
    <div>
        <div class="slider-form">
            <input type="time" v-model="startTime" :max="endTime" min="00:00">
            -
            <input type="time" v-model="endTime" max="24:00" :min="startTime">
        </div>
        <div class="slider-wrapper" ref="sliderWrapper">
            <div class="slider-circle slider-circle-left"
                 ref="sliderCircleLeft"
                 @mousedown="dragStart('left')"
                 :style="{transform: 'translate('+ posLeft+'px, -25%)'}"></div>
            <div class="slider-circle slider-circle-right"
                 ref="sliderCircleRight"
                 @mousedown="dragStart('right')"
                 :style="{transform: 'translate('+ (posRight-20)+'px, -25%)'}"></div>
            <div class="slider-line" ref="sliderLine"></div>
            <div class="slider-line-selected" :style="{transform: 'translateX('+ (posLeft)+'px)', width: widthSelected + 'px'}"></div>
        </div>
    </div>
</template>

<script>
    import moment from 'moment';

    export default {
        name: "Slider",
        data:()=>({
            left:25,
            right:75,
            posLeft:0,
            posRight:0,
            widthSelected:0,
            startTime:'00:00',
            endTime:'00:00',
        }),
        mounted() {
            this.calculate();
            this.$nextTick(function() {
                this.bindListener();
            });
        },
        watch:{
            startTime(val){
                let maxMinutes = 1440;
                let curMin = moment(val,'HH:mm').hours()*60+moment(val,'HH:mm').minutes();
                this.left = (100 * curMin)/ maxMinutes;
            },
            endTime(val){
                let maxMinutes = 1440;
                let curMin = moment(val,'HH:mm').hours()*60+moment(val,'HH:mm').minutes();
                this.right = (100 * curMin)/ maxMinutes;
            }
        },
        methods:{
            bindListener: function() {
                document.addEventListener("mousemove", (e)=>this.drag(e));
                document.addEventListener("mouseup", (e)=>this.dragEnd(e));
                window.addEventListener("resize", ()=>this.calculate());
            },
            dragStart: function(circle) {
                this.draggingRight = false;
                this.draggingLeft = false;
                switch(circle){
                    case 'left':
                        this.draggingLeft = true;
                        break;
                    case 'right':
                        this.draggingRight = true;
                        break;
                }
            },
            drag: function(ev) {
                if(this.draggingLeft)
                    this.calculateLeft(ev);

                if(this.draggingRight)
                    this.calculateRight(ev);

                if(this.draggingRight || this.draggingLeft)
                    this.calculate();
            },
            calculateLeft(ev){
                let mouseX = ev.clientX;
                let wrapperX = this.$refs.sliderWrapper && this.$refs.sliderWrapper.offsetLeft;
                let lineX = this.$refs.sliderLine && this.$refs.sliderLine.clientWidth;
                let circleRightX = this.$refs.sliderCircleRight && this.$refs.sliderCircleRight.getBoundingClientRect().left;
                if(mouseX < wrapperX || mouseX > circleRightX-20)
                    return;

                this.left = 100 * (mouseX - wrapperX) / lineX;
            },
            calculateRight(ev){
                let mouseX = ev.clientX;
                let wrapperX = this.$refs.sliderWrapper && this.$refs.sliderWrapper.offsetLeft;
                let lineX = this.$refs.sliderLine && this.$refs.sliderLine.clientWidth;
                let circleLeftX = this.$refs.sliderCircleLeft && this.$refs.sliderCircleLeft.getBoundingClientRect().left;

                if(mouseX > wrapperX + this.$refs.sliderWrapper.clientWidth || mouseX < circleLeftX+30)
                    return;

                this.right = (100 * (mouseX - wrapperX)) / lineX;
            },
            dragEnd: function() {
                this.draggingRight = false;
                this.draggingLeft = false;
            },
            calculate(){
                let width = this.$refs.sliderLine.clientWidth;

                this.posLeft = (width * this.left)/100;
                this.posRight = (width * this.right)/100;

                this.widthSelected = this.posRight - this.posLeft;

                this.initStartTime();
                this.initEndTime();
            },
            initStartTime(){
                let maxMinutes = 1440;
                let curMin = (maxMinutes * this.left) / 100;
                this.startTime = moment('00:00','HH:mm').add(curMin,'minutes').format('HH:mm');
            },
            initEndTime(){
                let maxMinutes = 1440;
                let curMin = (maxMinutes * (this.right)) / 100;
                this.endTime = moment('00:00','HH:mm').add(curMin,'minutes').format('HH:mm');
            }
        }
    }
</script>

<style scoped>
    .slider-wrapper{
        position: relative;
    }
    .slider-form{
        margin-bottom: 10px;
    }
    .slider-line,
    .slider-line-selected{
        height:10px;
        background-color: #ccc;
        width: 100%;
        border-radius: 5px;
    }
    .slider-line-selected{
        position: absolute;
        background-color: #990100;
        top: 0px;
    }
    .slider-circle{
        width: 20px;
        height: 20px;
        background-color: #fff;
        box-shadow: 0px 0px 16px -5px #000;
        border-radius: 50%;
        position: absolute;
        top: 0px;
        z-index: 1;
        cursor: pointer;
    }
</style>
