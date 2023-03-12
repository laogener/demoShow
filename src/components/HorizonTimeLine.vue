<template>
    <div class="Timeline">
        <div class="timeaxis">
            <div v-for="(item,i) in list" :key="i">
                <div class="timeaxis-box">
                    <div class="timeaxis-topText" :class="{'bd-empty':i==list.length-1}">
                        <div class="text">{{item.warnname}}</div>
<!--                        <div class="tiem">2017-03-10</div>-->
                    </div>
                    <div v-if="active == i" class="dtgy">
                        <div class="one"><p></p><span></span></div>
                    </div>
                    <div v-else class="circular"></div>

                    <div class="timeaxis-bootomText">
                        <div class="text">{{item.standard}}</div>
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
    .timeaxis {
        display: flex;
        .timeaxis-box {
            width: 124px;
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
                .tiem {
                    position: absolute;
                    top: -35px;
                    font-size: 14px;
                    color: #9ba3ad;
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
            }
        }
    }
}

</style>
