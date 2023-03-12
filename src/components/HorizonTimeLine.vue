<template>
    <div class="Timeline">
        <div class="timeaxis">
            <div v-for="(item,i) in list" :key="i">
                <div class="timeaxis-box">
                    <div class="timeaxis-topText" :class="{'bd-empty':i==list.length-1}">
                        <div class="text" :class="{'color_165dff':active == i}">{{item.warnname}}</div>
                    </div>
                    <div v-if="active == i" class="dtgy">
                        <div class="one"><p></p><span></span></div>
                    </div>
                    <div v-else class="circular"></div>

                    <div class="timeaxis-bootomText">
                        <template v-if="moreLine">
                            <div class="margin_b_10 addr">
                                <el-tooltip class="item" effect="dark" :content="item.standard" placement="top">
                                    <span class="line1_2 bolder" :class="{'color_165dff':active == i}">{{item.standard}}</span>
                                </el-tooltip>
                            </div>
                            <div class="time">
                                <span class="tag2 real">实</span>
                                <span :class="{'color_165dff':active == i}">{{item.time}}</span>
                            </div>
                        </template>
                        <div v-else class="text" :class="{'color_165dff':active == i}">{{item.standard}}</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>
<script>
export default {
    name: 'HorizonTimeLine',
    props: {
        list: { // 时间轴数据
            type: Array,
            default: () => []
        },
        active: { // 初始选中
            type: Number,
            default: -1
        },
        moreLine: { // 多行
            type: Boolean,
            default: false
        }
    },
    data () {
        return {
        }
    },
    methods: {

    }
}
</script>
<style lang="scss" scoped>
.Timeline {
    margin-top: 40px;
    height: 48px;
    .timeaxis {
        display: flex;
        .timeaxis-box {
            width: 164px;
            .circular {
                width: 12px;
                height: 12px;
                border-radius: 8px;
                background: #165dff;
                margin-bottom: 4px;
                position: relative;
                top: -6px;
                box-shadow: 0px 0px 5px 5px #fff;
            }
            .timeaxis-topText {
                border-bottom: 1px solid #155eff4d;
                position: relative;
                margin: 0 10px;
                .text {
                    position: absolute;
                    top: -35px;
                    left: -14px;
                }

            }
            .bd-empty {
                border: 0;
            }
            .timeaxis-bootomText {
                position: relative;
                .text {
                    position: absolute;
                    top: 10px;
                    font-size: 14px;
                    color: #9ba3ad;
                }
                .addr {
                    position: absolute;
                    top: 10px;
                    font-size: 14px;
                }
                .time {
                    position: absolute;
                    top: 34px;
                    font-size: 14px;
                    color: #9ba3ad;
                }
                .tag2 {
                    border-radius: 50%;
                    font-size: 12px;
                    padding: 3px;
                    font-weight: 700;
                    line-height: 1;
                }
                .real{
                    background-color: #44d7b633;
                    color: #33cfac;
                }
            }
        }
    }
}

</style>
