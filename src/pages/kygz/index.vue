<template>
    <div>
        <!--        顶部搜索-->
        <div class="margin_b_20">
            <el-input size="small" class="margin_r_16" placeholder="输入运单号" style="width: 340px" v-model="queryData.a" clearable></el-input>
            <el-button type="warning" size="small">订阅</el-button>
            <el-button type="text" @click="dialog = true">查看航司</el-button>
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
                    <el-col :span="5">运单号：157-76794874</el-col>
                    <el-col :span="5">航空公司：卡塔尔航空</el-col>
                    <el-col :span="9">
                        <span>航程：</span>
                        <span>PVG</span>
                        <el-divider class="divider" content-position="center">中转(2)</el-divider>
                        <span>AMS</span>
                    </el-col>
                    <el-col :span="5">总件/总重量：36pc/553kg</el-col>
                </el-row>
                <div class="padding_20 color_00b26f">
                    当前状态：SDD/货物已提取 2022-05-04 12:22
                </div>
            </div>
            <el-row :gutter="20" class="padding_20">
                <el-col :span="12">
                    <div class="margin_b_20 bolder size16">货物动态</div>
                    <el-timeline>
                        <el-timeline-item v-for="(item,index) in timelineArr" :key="index" color="#165dff" placement="top">
                            <el-card>
                                <div class="flex">
                                    <span class="bolder" :class="{'color_165dff': !index}">{{item.a}}</span>
                                    <span></span>
                                    <span>
                                        <span class="tag2 real margin_r_4">实</span>
                                        <span :class="{'color_165dff': !index}">{{item.b}}</span>
                                    </span>
                                </div>
                                <div class="flex">
                                    <span>地点: {{item.c}}</span>
                                    <span>
                                        <template v-if="item.d">航班:{{item.d}}</template>
                                    </span>
                                    <span>件/重量:{{item.e}}</span>
                                </div>
                            </el-card>
                        </el-timeline-item>
                    </el-timeline>
                </el-col>
                <el-col :span="12">
                    <div class="margin_b_20 bolder size16">航班信息</div>

                    <div class="shadow">
                        <div class="padding_20 border_b">
                            <div class="margin_b_10">
                                <span class="margin_r_80">航班: QR-0273</span>
                                <span>
                                    <el-radio class="margin_0"></el-radio>
                                    <span>出发: DOH</span>
                                    <span class="middleLine"></span>
                                    <span>到达: AMS</span>
                                </span>
                            </div>
                            <div class="margin_b_10">航班日期: 2022-05-03</div>
                            <el-row :gutter="20">
                                <el-col :span="12" class="border_r">
                                    <el-timeline>
                                        <el-timeline-item
                                            v-for="(activity, index) in activities"
                                            color="#165dff"
                                            :key="index">
                                            {{activity.content}}
                                        </el-timeline-item>
                                    </el-timeline>
                                </el-col>
                                <el-col :span="12">
                                    <el-timeline>
                                        <el-timeline-item
                                            v-for="(activity, index) in activities"
                                            color="#165dff"
                                            :key="index">
                                            {{activity.content}}
                                        </el-timeline-item>
                                    </el-timeline>
                                </el-col>
                            </el-row>
                        </div>
                        <div class="padding_20 border_b">
                            <div class="margin_b_10">
                                <span class="margin_r_80">航班: QR-0273</span>
                                <span>
                                    <el-radio class="margin_0"></el-radio>
                                    <span>出发: DOH</span>
                                    <span class="middleLine"></span>
                                    <span>到达: AMS</span>
                                </span>
                            </div>
                            <div class="margin_b_10">航班日期: 2022-05-03</div>
                            <el-row :gutter="20">
                                <el-col :span="12" class="border_r">
                                    <el-timeline>
                                        <el-timeline-item
                                            v-for="(activity, index) in activities"
                                            color="#165dff"
                                            :key="index">
                                            {{activity.content}}
                                        </el-timeline-item>
                                    </el-timeline>
                                </el-col>
                                <el-col :span="12">
                                    <el-timeline>
                                        <el-timeline-item
                                            v-for="(activity, index) in activities"
                                            color="#165dff"
                                            :key="index">
                                            {{activity.content}}
                                        </el-timeline-item>
                                    </el-timeline>
                                </el-col>
                            </el-row>
                        </div>
                        <div class="padding_20">
                            <div class="margin_b_10">
                                <span class="margin_r_80">航班: QR-0273</span>
                                <span>
                                    <el-radio class="margin_0"></el-radio>
                                    <span>出发: DOH</span>
                                    <span class="middleLine"></span>
                                    <span>到达: AMS</span>
                                </span>
                            </div>
                            <div class="margin_b_10">航班日期: 2022-05-03</div>
                            <el-row :gutter="20">
                                <el-col :span="12" class="border_r">
                                    <el-timeline>
                                        <el-timeline-item
                                            v-for="(activity, index) in activities"
                                            color="#165dff"
                                            :key="index">
                                            {{activity.content}}
                                        </el-timeline-item>
                                    </el-timeline>
                                </el-col>
                                <el-col :span="12">
                                    <el-timeline>
                                        <el-timeline-item
                                            v-for="(activity, index) in activities"
                                            color="#165dff"
                                            :key="index">
                                            {{activity.content}}
                                        </el-timeline-item>
                                    </el-timeline>
                                </el-col>
                            </el-row>
                        </div>
                    </div>
                </el-col>
            </el-row>
        </div>
        <div v-else>
            <div class="margin_b_20 size16 bolder">订阅示例</div>

            <!--        提单信息-->
            <div class="shadow">
                <div class="top margin_b_20">
                    <img class="slsj" src="@/assets/image/slsj.png" alt="">
                </div>
                <el-row :gutter="20" class="padding_20 border_b">
                    <el-col :span="5">
                        <el-checkbox class="margin_r_4" disabled></el-checkbox>
                        运单号：157-76794874
                    </el-col>
                    <el-col :span="5">航空公司：卡塔尔航空</el-col>
                    <el-col :span="9">
                        <span>PVG</span>
                        <el-divider class="divider" content-position="center">中转(2)</el-divider>
                        <span>AMS</span>
                    </el-col>
                    <el-col :span="5">总件/总重量：36pc/553.000kg</el-col>
                </el-row>
                <div class="padding_20 border_b">
                    <HorizonTimeLine :list="list" :active="6"/>
                </div>
                <div class="padding_20">
                    <span> 录入员工：张三</span>
                    <span class="float_r margin_t-8">
                    <span class="margin_r_80 color_00b26f">数据更新时间：2022-09-08 13:54</span>
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
<!--        查看航司弹窗-->
        <el-dialog title="查看航司" :visible.sync="dialog">
            <div class="margin_b_20">
                <el-input
                    style="width: 400px"
                    placeholder="搜索航司名称，目前已支持58家航司订阅"
                    prefix-icon="el-icon-search"
                    v-model="input2">
                </el-input>
            </div>
            <el-table :data="gridData"
                      height="250"
                      style="width: 100%">
                <el-table-column
                    type="index"
                    label="序号"
                    width="50">
                </el-table-column>
                <el-table-column property="a" label="航司二字码"></el-table-column>
                <el-table-column property="b" label="提单代码"></el-table-column>
                <el-table-column property="c" label="航司中文名"></el-table-column>
            </el-table>
        </el-dialog>
    </div>
</template>

<script>
import HorizonTimeLine from '@/components/HorizonTimeLine'

export default {
    data() {
        return {
            queryData: {
                a: '',
            },
            list: [
                {
                    warnname: "订舱",
                    standard: '-',
                },
                {
                    warnname: "进仓",
                    standard: '2022-05-01 20:00',
                },
                {
                    warnname: "起飞",
                    standard: '2022-05-02 12:58',
                },
                {
                    warnname: "中转抵达",
                    standard: '2022-05-02 21:22',
                },
                {
                    warnname: "中转起飞",
                    standard: '2022-05-03 08:17',
                },
                {
                    warnname: "抵达",
                    standard: '2022-05-03 13:50',
                },
                {
                    warnname: "提货",
                    standard: '2022-05-04 12:22',
                },
            ],
            showDetail: false,
            timelineArr:[
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'QR0273',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'QR0273',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
                {
                    a:'SDD/货物已提取',
                    b:'2022-05-04 12:22',
                    c:'AMS',
                    d:'',
                    e:'36pc/553kg',
                },
            ],
            activities: [
                {content: '计划起飞时间：2022-07-01 22:30'},
                {content: '预计起飞时间：2022-07-04 14:30'},
                {content: '实际起飞时间：2022-07-04 14:30'}
            ],
            gridData: [
                {
                    a:'AA',
                    b:'001',
                    c:'美航',
                },
                {
                    a:'AA',
                    b:'001',
                    c:'美航',
                },
                {
                    a:'AA',
                    b:'001',
                    c:'美航',
                },
                {
                    a:'AA',
                    b:'001',
                    c:'美航',
                },
                {
                    a:'AA',
                    b:'001',
                    c:'美航',
                },
                {
                    a:'AA',
                    b:'001',
                    c:'美航',
                },
            ],
            dialog: false,
            input2:''
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
.divider{
    display: inline-block;
    width: 66%;
    vertical-align: middle;
    margin: 0 8px;
}
.middleLine {
    display: inline-block;
    position: relative;
    top: -5px;
    width: 40px;
    height: 1px;
    background-color: #d8d8d8;
    margin: 0 20px;
}
.top {
    position: relative;
    border-radius: 4px;
}

.flex{
    display: flex;
    margin-bottom: 10px;
    >span{
        flex: 1;
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
</style>
