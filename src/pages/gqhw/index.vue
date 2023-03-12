<template>
    <div>
        <!--        顶部搜索-->
        <div class="margin_b_20">
            <el-select size="small" class="margin_r_16" v-model="queryData.a" placeholder="选择港区">
                <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                    <span style="float: left">{{ item.label }}</span>
                    <span style="float: right; color: #8492a6; font-size: 13px">{{ item.value }}</span>
                </el-option>
            </el-select>
            <el-input size="small" class="margin_r_16" style="width: 180px" placeholder="输入提单号(必填)" v-model="queryData.b" clearable></el-input>
            <el-input size="small" placeholder="输入船名" style="width: 240px" v-model="queryData.c" clearable></el-input>
            <el-input size="small" class="margin_r_16" placeholder="输入航次" style="width: 140px" v-model="queryData.d" clearable></el-input>
            <el-radio class="margin_r_16" v-model="queryData.e" label="1">出口</el-radio>

            <el-button type="warning" size="small">订阅</el-button>
            <el-button type="primary" size="small" class="margin_r_16">批量订阅</el-button>
            <el-link type="primary">批量订阅记录</el-link>
        </div>

        <div v-if="showDetail">
            <div>
                <el-button type="text" @click="showDetail = !showDetail"><i class="el-icon-arrow-left"></i>返回
                </el-button>
            </div>
            <div class="shadow margin_b_20">
                <div class="top margin_b_20">
                    <img class="slsj2" src="@/assets/image/slsj2.png" alt="">
                </div>
                <el-row :gutter="20" class="padding_20 border_b">
                    <el-col :span="6">订阅号：OOLU2134397260</el-col>
                    <el-col :span="6">总箱数：4箱 （4*20' GP 8'6''）</el-col>
                </el-row>
                <el-row class="padding_20 border_b">
                    <el-col :span="5" class="border_r padding_r_10">
                        <el-timeline>
                            <el-timeline-item
                                v-for="(activity, index) in activities2"
                                size="large"
                                color="#165dff"
                                icon="el-icon-location"
                                :key="index">
                                {{activity.content}}
                            </el-timeline-item>
                        </el-timeline>
                    </el-col>
                    <el-col :span="19" class="padding_l_20 overflow_x">
                        <HorizonTimeLine :list="list" :active="4"/>

                    </el-col>
                </el-row>
            </div>

            <div class="margin_b_20 bolder size16">港口船计划信息</div>
            <div class="shadow margin_b_20">
                <el-row :gutter="20" class="padding_20 border_b">
                    <el-col :span="6">码头：振东(外2)</el-col>
                    <el-col :span="6">
                        <span class="margin_r_16">船：YM EXPRESS / 066W</span>
                        <el-button type="text">查看定位</el-button>
                    </el-col>
                </el-row>
                <el-row class="padding_20 border_b">
                    <el-col :span="6" class="border_r">
                        <el-timeline>
                            <el-timeline-item
                                v-for="(activity, index) in activities3"
                                color="#165dff"
                                :key="index">
                                {{activity.content}}
                            </el-timeline-item>
                        </el-timeline>
                    </el-col>
                    <el-col :span="6" class="border_r padding_l_20">
                        <el-timeline>
                            <el-timeline-item
                                v-for="(activity, index) in activities4"
                                color="#165dff"
                                :key="index">
                                {{activity.content}}
                            </el-timeline-item>
                        </el-timeline>
                    </el-col>
                    <el-col :span="6" class="border_r padding_l_20">
                        <el-timeline>
                            <el-timeline-item
                                v-for="(activity, index) in activities5"
                                color="#165dff"
                                :key="index">
                                {{activity.content}}
                            </el-timeline-item>
                        </el-timeline>
                    </el-col>
                    <el-col :span="6" class="padding_l_20">
                        <el-timeline>
                            <el-timeline-item
                                v-for="(activity, index) in activities6"
                                color="#165dff"
                                :key="index">
                                {{activity.content}}
                            </el-timeline-item>
                        </el-timeline>
                    </el-col>
                </el-row>
            </div>
            <div class="margin_b_20 bolder size16">集装箱信息（4）</div>
            <el-table
                :data="tableData"
                height="250"
                border
                style="width: 100%">
                <el-table-column
                    prop="a"
                    label="箱号"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="b"
                    label="封号"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="c"
                    label="箱型"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="d"
                    label="进场"
                    width="160">
                </el-table-column>
                <el-table-column
                    prop="e"
                    label="VGM码头称重"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="f"
                    label="运抵状态"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="g"
                    label="海放"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="h"
                    label="码放"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="i"
                    label="配载"
                    width="120">
                </el-table-column>
                <el-table-column
                    prop="j"
                    label="装船"
                    width="120">
                </el-table-column>
            </el-table>
        </div>
        <div v-else>
            <div class="margin_b_20 size16 bolder">订阅示例</div>

            <!--        提单信息-->
            <div class="shadow">
                <div class="top margin_b_20">
                    <img class="slsj" src="@/assets/image/slsj.png" alt="">
                </div>
                <el-row :gutter="20" class="padding_20 border_b">
                    <el-col :span="6">
                        <el-checkbox class="margin_r_4" disabled></el-checkbox>
                        订阅号：OOLU2134397260
                    </el-col>
                    <el-col :span="6">船名：YM EXPRESS/066W</el-col>
                    <el-col :span="6">起运港：CNSHA</el-col>
                    <el-col :span="6">目的港：PKKHI</el-col>
                </el-row>
                <el-row class="padding_20 border_b">
                    <el-col :span="5" class="border_r padding_r_10">
                        <el-timeline>
                            <el-timeline-item
                                v-for="(activity, index) in activities"
                                :color="'#165dff'"
                                :key="index">
                                {{activity.content}}
                            </el-timeline-item>
                        </el-timeline>
                    </el-col>
                    <el-col :span="19" class="padding_l_20 overflow_x">
                        <HorizonTimeLine :list="list" :active="4"/>

                    </el-col>
                </el-row>
                <div class="padding_20">
                    <span> 录入员工：张三</span>
                    <span class="float_r margin_t-8">
                    <span class="margin_r_80 color_67C23A">数据更新时间：2022-07-08 11:40</span>
                    <span>
                        <el-button type="text" disabled>取消提醒</el-button>
                        <el-button class="margin_r_16" type="text" disabled>设置提醒</el-button>
                        <el-button type="text" @click="showDetail = !showDetail">详情<i
                            class="el-icon-arrow-right"></i></el-button>
                    </span>
                </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import HorizonTimeLine from '@/components/HorizonTimeLine'

export default {
    data() {
        return {
            queryData: {
                a: '',
                b: '',
                c: '',
                d: '',
                e: '1',
            },
            options: [
                {
                    value: 'CNSHA',
                    label: '上海'
                }, {
                    value: 'CNTXG',
                    label: '天津'
                }, {
                    value: 'CNNGB',
                    label: '宁波,浙江'
                }
            ],
            activities: [
                {content: '预计开航：2022-07-04 14:30'},
                {content: '实际开航：2022-07-04 14:30'}
            ],
            activities2: [
                {content: 'CNSHA'},
                {content: 'PKKHI'}
            ],
            activities3: [
                {content: '进箱开始：2022-07-01 22:30'},
                {content: '进箱截止：2022-07-04 14:30'}
            ],
            activities4: [
                {content: '预计到港：2022-07-01 19:00'},
                {content: '实际到港：2022-07-01 19:00'}
            ],
            activities5: [
                {content: '预计靠泊：2022-07-03 14:30'},
                {content: '实际靠泊：2022-07-03 15:00'}
            ],
            activities6: [
                {content: '预计离泊：2022-07-04 14:30'},
                {content: '实际离泊：2022-07-04 14:30'}
            ],
            showQuery: false,

            list: [
                {
                    warnname: "进场",
                    standard: '4/4箱',
                },
                {
                    warnname: "海放",
                    standard: '4/4箱',
                },
                {
                    warnname: "码放",
                    standard: '4/4箱',
                },
                {
                    warnname: "配载",
                    standard: '4/4箱',
                },
                {
                    warnname: "装船",
                    standard: '4/4箱',
                },
            ],
            showDetail: false,
            hideDetail: false,
            list2: [
                {
                    warnname: "还空",
                    standard: 'Global Container Services 1,Doel,Vlaanderen,Belgium',
                    time: '2022/06/23 10:59',
                },
                {
                    warnname: "提货",
                    standard: 'Antwerp Gateway N.V. Quay 1700,Antwerp,Vlaanderen,Belgium',
                    time: '2022/06/21 10:25',
                },
                {
                    warnname: "卸载",
                    standard: 'Antwerp Gateway N.V. Quay 1700,Antwerp,Vlaanderen,Belgium',
                    time: '2022/06/12 01:16',
                },
                {
                    warnname: "装船",
                    standard: 'Tianjin Port Pacific Int\'l Ctn Tml,Xingang,Tianjin,China',
                    time: '2022/04/30 18:00',
                },
                {
                    warnname: "进场",
                    standard: 'Tianjin Port Pacific Int\'l Ctn Tml,Xingang,Tianjin,China',
                    time: '2022/04/27 11:51',
                },
                {
                    warnname: "提箱",
                    standard: 'Tianjin Binhai Cosco, Earth Port,Xingang,Tianjin,China',
                    time: '2022/04/22 07:26',
                },

            ],
            tableData: [
                {
                    a: 'OOLU0359488',
                    b: 'OOLHFV8361',
                    c: "20' GP 8'6''",
                    d: '2022-07-02 04:36:00',
                    e: '',
                    f: 'Y',
                    g: 'Y',
                    h: 'Y',
                    i: 'Y',
                    j: '2022-07-04 02:07:00',
                },
                {
                    a: 'OOLU0359488',
                    b: 'OOLHFV8361',
                    c: "20' GP 8'6''",
                    d: '2022-07-02 04:36:00',
                    e: '',
                    f: 'Y',
                    g: 'Y',
                    h: 'Y',
                    i: 'Y',
                    j: '2022-07-04 02:07:00',
                },
                {
                    a: 'OOLU0359488',
                    b: 'OOLHFV8361',
                    c: "20' GP 8'6''",
                    d: '2022-07-02 04:36:00',
                    e: '',
                    f: 'Y',
                    g: 'Y',
                    h: 'Y',
                    i: 'Y',
                    j: '2022-07-04 02:07:00',
                },
                {
                    a: 'OOLU0359488',
                    b: 'OOLHFV8361',
                    c: "20' GP 8'6''",
                    d: '2022-07-02 04:36:00',
                    e: '',
                    f: 'Y',
                    g: 'Y',
                    h: 'Y',
                    i: 'Y',
                    j: '2022-07-04 02:07:00',
                },
            ]
        }
    },
    created() {

    },
    methods: {},
    components: {
        HorizonTimeLine
    }
}
</script>

<style lang="scss" scoped>
.top {
    position: relative;
    border-radius: 4px;
}

.box{
    padding-bottom: 40px;
}
</style>
