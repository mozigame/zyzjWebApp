<template>
    <div>

        <div v-for="item in kjnumArr" :key="item.KJArr">
            
            <div class="contentCell">
                <span class="top-left">{{"第"+item.ID+"期"}}</span>
                <span class="top-right">{{item.CreateTime}}</span>
            </div>

            <div class="KJnum">
                <div v-show="isLan(index1)" v-for="(item1,index1) in item.Data.split(',')" :key="item1" :style="{width:ojwidth+'px',height:ojwidth+'px'}">
                    <div class="num">{{item1}}</div>
                </div>
                <div v-show="!isLan(index1)" v-for="(item1,index1) in item.Data.split(',')" :key="item1" :style="{width:ojwidth+'px',height:ojwidth+'px'}">
                    <div class="num1">{{item1}}</div>
                </div>
            </div>
            <div class="top"></div>
            <!-- <div class="top"></div> -->
        </div>

    </div>
</template>

<script>
export default {
    props: {
        data: {
            type: Array,
        }
    },

    data() {
        return {
            kjArr: "",
            height: 35,
            screenWidth: document.body.clientWidth
        }
    },

    methods:{
        isLan(index){
            if(index === 20){
                return false;
            }else {
                return true;
            }
        }
    },
    mounted() {
        const that = this
        window.onresize = () => {
            return (() => {
                window.screenWidth = document.body.clientWidth
                that.screenWidth = window.screenWidth
            })()
        }

    },
    watch: {
        screenWidth(val) {
            if (!this.timer) {
                this.screenWidth = val
                this.timer = true
                let that = this
                setTimeout(function() {
                    that.timer = false
                }, 400)
            }
        }
    },

    computed: {
        kjnumArr: {
            get: function() {

                return this.data;
            },
            set(){

            }
        },
        ojwidth: {
            // getter
            get: function() {
               var ojwidth;
                var margin;
                var colnum = 10;//列
                colnum = this.kjnumArr.length > colnum ? colnum : this.kjnumArr.length;
                var rownum = this.kjnumArr.length / colnum;//行
                margin = this.kjnumArr.length > 5 ? 1 : 2;//间距
                ojwidth = (this.screenWidth - (2 * (margin) * colnum)) / colnum;//格子的宽
                return ojwidth;
            },
            // setter
            set: function(newValue) {

            }
        }
    }

}
</script>

<style lang="less" scoped>
.contentCell {
    margin-top: 5px;
    margin-bottom: 5px;
    display: flex;
    justify-content: space-between;
}

.top-left {
    // background-image: url('../../../static/images/history/Records-02.png');
    font-size: 14px;
    font-weight: 400;
    margin-top: 5px;
    padding: 3px 15px 3px 5px;
    background-repeat: no-repeat;
    background-size: 100% 100%;
    color: gray;

    // margin-top: 5px;
}

.top-right {
    display: flex;
    align-items: center;
    font-size: 14px;
    font-weight: 400;
    margin-top: 5px;
    margin-right: 5px;
    color: gray;
}

.KJnum {
    margin: 5px 0px 5px 0px;
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    text-align: center;
}

.num {
    margin: 0px 5px;
    line-height: 27px;
    height: 27px;
    width: 27px;
    background-repeat: no-repeat;

    background-size: 27px;
    color: white;
    font-size: 15px;
    background-image: url('../../../static/images/quan2.png');
}

.num1 {
    margin: 0px 5px;
    line-height: 27px;
    height: 27px;
    width: 27px;
    background-repeat: no-repeat;

    background-size: 27px;
    color: white;
    font-size: 15px;
    background-image: url('../../../static/images/quan2-1.png');
}

.top {
    height: 1px;
    background:RGB(243, 244, 245);
}
</style>

