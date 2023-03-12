<template>
    <div class="padding_20">
        <!--        顶部搜索-->
        <div class="margin_b_20">
            <el-input size="small" class="margin_r_16" :placeholder="'请输入' + placeholder" style="width: 450px"
                      v-model="queryData.a">
                <el-select @change="selectChange" v-model="queryData.b" slot="prepend" style="width: 130px"
                           placeholder="请选择">
                    <el-option label="提单号" value="1"></el-option>
                    <el-option label="箱号" value="2"></el-option>
                    <el-option label="订舱号" value="3"></el-option>
                </el-select>
            </el-input>
            <el-select size="small" class="margin_r_16" v-model="queryData.c" placeholder="搜索船司">
                <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                </el-option>
            </el-select>
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
                <el-descriptions class="padding_20" :column="4">
                    <el-descriptions-item label="提单号">6331817980</el-descriptions-item>
                    <el-descriptions-item label="订舱号">-</el-descriptions-item>
                    <el-descriptions-item label="船司">COSCO</el-descriptions-item>
                    <el-descriptions-item label="箱量">1*40HQ</el-descriptions-item>
                    <el-descriptions-item label="起运地">
                        <el-tooltip class="item" effect="dark" content="Xingang,TJ,Tianjin,China" placement="top">
                            <span class="line1">Xingang,TJ,Tianjin,China</span>
                        </el-tooltip>
                    </el-descriptions-item>
                    <el-descriptions-item label="起运港">
                        <el-tooltip class="item" effect="dark" content="Xingang-Tianjin Port Pacific Int'l Ctn Tml"
                                    placement="top">
                            <span class="line1">Xingang-Tianjin Port Pacific Int'l Ctn Tml</span>
                        </el-tooltip>
                    </el-descriptions-item>
                    <el-descriptions-item label="目的港">
                        <el-tooltip class="item" effect="dark" content="Antwerp-Antwerp Gateway N.V. Quay 1700"
                                    placement="top">
                            <span class="line1">Antwerp-Antwerp Gateway N.V. Quay 1700</span>
                        </el-tooltip>
                    </el-descriptions-item>
                    <el-descriptions-item label="目的地">
                        <el-tooltip class="item" effect="dark" content="Antwerp,Antwerpen,Belgium" placement="top">
                            <span class="line1">Antwerp,Antwerpen,Belgium</span>
                        </el-tooltip>
                    </el-descriptions-item>
                    <el-descriptions-item label="ETD">2022-04-30 23:00:00</el-descriptions-item>
                    <el-descriptions-item label="ATD">2022-04-30 20:30:00</el-descriptions-item>
                    <el-descriptions-item label="ETA">2022-06-10 15:00:00</el-descriptions-item>
                    <el-descriptions-item label="ATA">2022-06-10 14:14:00</el-descriptions-item>
                </el-descriptions>
            </div>

            <div class="margin_b_20 bolder size16">集装箱信息（1）</div>
            <div class="shadow relative hidden">
                <div class="tag"></div>
                <div class="padding_20">
                    <span class="margin_r_80 bolder">箱号：FFAU2752798</span>
                    <span class="margin_r_80 bolder">箱型：40HQ</span>
                    <span class="color_409EFF pointer" @click="hideDetail = !hideDetail">
                      最新动态：
                       <el-tooltip class="item" effect="dark" content="2022/06/23 10:59，还空，Global Container Services 1,Doel,Vlaanderen,Belgium" placement="top">
                           <span class="line1">2022/06/23 10:59，还空，Global Container Services 1,Doel,Vlaanderen,Belgium</span>
                       </el-tooltip>
                        <i :class="hideDetail ? 'el-icon-caret-right' : 'el-icon-caret-bottom'"></i>
                    </span>
                </div>
                <div class="padding_20 border_t box overflow_x" v-if="!hideDetail">
                    <HorizonTimeLine :list="list2" :active="5" :moreLine="true"/>
                </div>
            </div>
        </div>
        <div v-else>
            <div class="margin_b_20 size16 bolder">订阅示例</div>

            <!--        详细搜索-->
            <div class="shadow padding_20 margin_b_40">
                <div v-if="showQuery" class="border_b margin_b_20">
                    <el-row class="margin_b_20" :gutter="20">
                        <el-col :span="12">
                            <el-autocomplete
                                size="small"
                                style="width: 100%"
                                v-model="queryData2.a"
                                :fetch-suggestions="querySearch"
                                placeholder="搜索船司"
                            >
                                <template slot="prepend">船司:</template>
                            </el-autocomplete>
                        </el-col>
                        <el-col :span="12">
                            <el-input size="small" placeholder="请输入内容" v-model="queryData2.b">
                                <template slot="prepend">单号/备注:</template>
                            </el-input>
                        </el-col>
                    </el-row>
                    <el-row class="margin_b_20" :gutter="20">
                        <el-col :span="12">
                            <el-row>
                                <el-col :span="5">
                                    <el-select size="small" v-model="queryData2.c" placeholder="搜索船司">
                                        <el-option
                                            v-for="item in options2"
                                            :key="item.value"
                                            :label="item.label"
                                            :value="item.value">
                                        </el-option>
                                    </el-select>
                                </el-col>
                                <el-col :span="19">
                                    <el-date-picker
                                        size="small"
                                        style="width: 100%"
                                        v-model="queryData2.d"
                                        type="datetimerange"
                                        align="right"
                                        range-separator="至"
                                        start-placeholder="开始日期"
                                        end-placeholder="结束日期"
                                        :default-time="['00:00:00', '23:59:59']">
                                    </el-date-picker>
                                </el-col>
                            </el-row>
                        </el-col>
                        <el-col :span="12">
                            <el-row>
                                <el-col :span="5">
                                    <el-select size="small" v-model="queryData2.e" placeholder="搜索船司">
                                        <el-option
                                            v-for="item in options3"
                                            :key="item.value"
                                            :label="item.label"
                                            :value="item.value">
                                        </el-option>
                                    </el-select>
                                </el-col>
                                <el-col :span="19">
                                    <el-date-picker
                                        size="small"
                                        style="width: 100%"
                                        v-model="queryData2.f"
                                        type="datetimerange"
                                        align="right"
                                        range-separator="至"
                                        start-placeholder="开始日期"
                                        end-placeholder="结束日期"
                                        :default-time="['00:00:00', '23:59:59']">
                                    </el-date-picker>
                                </el-col>
                            </el-row>
                        </el-col>
                    </el-row>
                    <el-row class="margin_b_20" :gutter="20">
                        <el-col :span="6">
                            <el-input size="small" placeholder="请输入" v-model="queryData2.g">
                                <template slot="prepend">船名:</template>
                            </el-input>
                        </el-col>
                        <el-col :span="6">
                            <el-input size="small" placeholder="请输入" v-model="queryData2.g">
                                <template slot="prepend">航次:</template>
                            </el-input>
                        </el-col>
                        <el-col :span="6">
                            <el-input size="small" placeholder="请输入" v-model="queryData2.g">
                                <template slot="prepend">起运港:</template>
                            </el-input>
                        </el-col>
                        <el-col :span="6">
                            <el-input size="small" placeholder="请输入" v-model="queryData2.g">
                                <template slot="prepend">目的港:</template>
                            </el-input>
                        </el-col>
                    </el-row>
                    <div class="text_r margin_b_20">
                        <el-button size="small" type="primary">查询</el-button>
                        <el-button size="small">清空</el-button>
                    </div>
                </div>
                <div class="text_c">
                <span class="pointer" @click="showQuery = !showQuery">
                    {{ showQuery ? '收起' : '展开' }}筛选项
                    <i class="el-icon-d-arrow-left" :class="{'rotate_90':!showQuery}"></i>
                </span>
                </div>
            </div>

            <!--        提单信息-->
            <div class="shadow">
                <div class="top margin_b_20">
                    <img class="wd" src="@/assets/image/wd.png" alt="">
                    <img class="slsj" src="@/assets/image/slsj.png" alt="">
                </div>
                <div class="padding_20 border_b">
                    <span class="margin_r_80">
                        <el-checkbox class="margin_r_4" disabled></el-checkbox>
                        提单号：COSU6331817980
                    </span>
                    <span>
                        <el-radio class="margin_0"></el-radio>
                        <span>
                            起运港：
                            <el-tooltip class="item" effect="dark" content="Xingang-Tianjin Port Pacific Int'l Ctn Tml"
                                        placement="top">
                             <span class="line1">Xingang-Tianjin Port Pacific Int'l Ctn Tml</span>
                            </el-tooltip>
                        </span>
                        <span class="middleLine"></span>
                        <span>
                            目的港：
                            <el-tooltip class="item" effect="dark" content="Antwerp-Antwerp Gateway N.V. Quay 1700"
                                        placement="top">
                             <span class="line1">Antwerp-Antwerp Gateway N.V. Quay 1700</span>
                            </el-tooltip>
                        </span>
                    </span>
                </div>
                <el-row class="padding_20 border_b">
                    <el-col :span="4" class="border_r padding_r_10">
                        <div class="margin_b_10">船司：COSCO</div>
                        <div class="margin_b_10">船名：THALASSA AVRA</div>
                        <div class="margin_b_10">航次：0600-041W</div>
                    </el-col>
                    <el-col :span="20" class="padding_l_20 overflow_x">
                        <HorizonTimeLine :list="list" :active="7"/>

                    </el-col>
                </el-row>
                <div class="padding_20">
                    <span> 录入员工：张三</span>
                    <span class="float_r margin_t-8">
                    <span class="margin_r_80 color_67C23A">数据更新时间：2022-07-08 11:34</span>
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
                b: '1',
                c: '',
            },
            placeholder: '提单号',
            options: [
                {
                    value: '兴亚航运(HAL)',
                    label: '兴亚航运(HAL)'
                }, {
                    value: '宏海箱运(RCL)',
                    label: '宏海箱运(RCL)'
                }, {
                    value: '正利航业(CNC)',
                    label: '正利航业(CNC)'
                }
            ],
            options2: [
                {
                    value: 'ETD',
                    label: 'ETD'
                }, {
                    value: 'ATD',
                    label: 'ATD'
                }
            ],
            options3: [
                {
                    value: 'ETA',
                    label: 'ETA'
                }, {
                    value: 'ATA',
                    label: 'ATA'
                }
            ],
            queryData2: {
                a: '',
                b: '',
                c: 'ETD',
                d: '',
                e: 'ETA',
                f: '',
                g: '',
                h: '',
                i: '',
                j: '',
            },
            showQuery: false,

            list: [
                {
                    warnname: "提箱",
                    standard: '1/1箱',
                },
                {
                    warnname: "进场",
                    standard: '1/1箱',
                },
                {
                    warnname: "装船",
                    standard: '1/1箱',
                },
                {
                    warnname: "开航",
                    standard: '1/1箱',
                },
                {
                    warnname: "抵港",
                    standard: '1/1箱',
                },
                {
                    warnname: "卸载",
                    standard: '1/1箱',
                },
                {
                    warnname: "提货",
                    standard: '1/1箱',
                },
                {
                    warnname: "还空",
                    standard: '1/1箱',
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
        }
    },
    created() {

    },
    methods: {
        querySearch(queryString, cb) {
            var restaurants = this.options;
            var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
            // 调用 callback 返回建议列表的数据
            cb(results);
        },
        createFilter(queryString) {
            return (restaurant) => {
                return (restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
            };
        },
        selectChange(val) {
            if (val == 1) {
                this.placeholder = '提单号'
            } else if (val == 2) {
                this.placeholder = '箱号'
            } else if (val == 3) {
                this.placeholder = '订舱号'
            }
        }
    },
    components: {
        HorizonTimeLine
    }
}
</script>

<style lang="scss" scoped>
.el-icon-d-arrow-left {
    transform: rotate(90deg);
}

.rotate_90 {
    transform: rotate(-90deg);
}

.top {
    position: relative;
    border-top: 2px solid #168BE8;
    border-radius: 4px;
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
.box{
    padding-bottom: 40px;
}

</style>
