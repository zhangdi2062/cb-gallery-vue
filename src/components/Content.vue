<template>
    <!-- 中间部分 -->
    <div v-if="isShow" class="index-content">
        <!-- 项目列表部分 -->
        <div id="content">
            <div class="itembox">
                <div class="item-title">
                    <h1 class="title container-fluid text-center">优锘科技</h1>
                    <h3 class="subtitle container-fluid text-center">
                        <!-- <hr class="linefloat line"> -->
                        ————— 可视化案例 —————
                        <!-- <div class="linefloat"></div> -->
                        <!-- <hr class="linefloat line"> -->
                    </h3>
                    <h3 class="subtitle container-fluid text-center">致力实现人性、智能、众创的可视化</h3>
                </div>
                <div id="search">
                    <div>
                        <ul class="searchType">
                            <li class="text-center data-search-industry" id="searchByIndustry">
                                <span>全部行业</span>
                                <ul class="industryList">
                                    <li onclick="orderList('industryall',this)">全部行业</li>
                                </ul>
                            </li>
                            <li class="text-center data-search-industry" id="searchByProduct">
                                <span>全部产品</span>
                                <ul class="industryList">
                                    <li onclick="orderList('productall',this)">全部产品</li>
                                </ul>
                            </li>
                            <li
                                class="text-center data-search-name"
                                onclick="orderList('name',this)"
                            >名称</li>
                            <li
                                class="text-center data-search-industry ascSort"
                                id="searchByDate"
                                onclick="orderList('date',this)"
                            >时间</li>

                            <li class="searchkey">
                                <div class="searchBox" id="searchBox">
                                    <input
                                        type="text"
                                        id="searchValue"
                                        placeholder="搜索可视化案例"
                                        onkeyup="return onKeyPress(event)"
                                    />
                                </div>
                            </li>
                            <li class="searchbtn text-right">
                                <img
                                    onclick="sortByKeywords()"
                                    class="closeSearch"
                                    src="/static/img//search1.png"
                                    width="24px"
                                    height="24px"
                                />
                            </li>
                        </ul>
                        <div class="bgline"></div>
                        <div
                            class="li-move"
                            style="height: 1px;width: 0px; background: #ff7f00; margin-top: -1px;"
                        ></div>
                    </div>
                    <aside
                        id="searchresults"
                        class="searchresults"
                        data-quicklinks="快速链接"
                        data-suggestions="搜索结果建议"
                        data-string-noresults
                    >
                        <section class="searchresults-section">
                            <div class="searchresults-section-wrapper">
                                <h3 class="searchresults-header"></h3>
                                <ul class="searchresults-list" id="defaultlinks"></ul>
                            </div>
                        </section>
                    </aside>
                </div>
                <div class="row item-row">
                    <template v-for="(item, index) in showData">
                        <Item :item="item" :index="index" :key="index"></Item>
                    </template>
                </div>
            </div>
            <div class="morebtn">
                <div class="more" style="letter-spacing: 2px;" @click="showMore">查看更多</div>
                <div class="nomore">没有更多了</div>
            </div>
            <div class="totop">
                <a href="#logo" id="totop" @click="totop"></a>
            </div>
        </div>
        <Detail></Detail>
    </div>
</template>

<script>
import Item from './Item';
import Detail from './Detail';

export default {
    name: 'Home',
    props: {
        msg: String,
    },
    data() {
        return {
            DEFAULT_LINKS_ARR: [
                '南网地理信息可视化项目',
                '建行南湖大屏可视化平台',
                '深圳交警集中运维可视化平台',
                '北京电力应急指挥大屏',
                '福州数字办可视化项目',
            ], //默认搜索快速链接名称
            DEFAULTPAGE: 12, //默认加载12条
            isShow: false,
            currData: [],
            showData: [],
            pageSize: 6, //每次加载条数
        };
    },
    components: {
        Detail,
        Item,
    },
    created() {
        this.$http.get('/static/json/mock.json').then(data => {
            this.currData = [...data.data];
            this.currData.sort(this.compareDesc('name'))
            this.currData.sort(this.compareDesc('date'))
            this.showData = this.currData.slice(0, 6);
        });
    },
    methods: {
        showMore() {
            this.showData = this.currData.slice(0, 12);
        },
        totop() {
            document.body.style.scrollTop = 10;
        },
        itemMouseenter() {
            this.itemMouse = true;
        },
        /**
         * @description 降序排序
         * @param {String} type 排序类型
         */
        compareDesc(type) {
            return function(item1, item2) {
                let key1 = item1.list[type];
                let key2 = item2.list[type];
                if (type === 'date') {
                    if (key1 > key2) return -1;
                    else if (key1 < key2) return 1;
                    else return 0;
                } else if (type === 'name') {
                    return key1.localeCompare(key2, 'zh');
                }
            };
        },

        /**
         * @description 升序排序
         * @param {String} type 排序类型
         */
        compareAsc(type) {
            return function(item1, item2) {
                let key1 = item1.list[type];
                let key2 = item2.list[type];
                if (type === 'date') {
                    if (key1 > key2) return 1;
                    else if (key1 < key2) return -1;
                    else return 0;
                }
            };
        },
    },
};
</script>

<style>
@keyframes bounceInUp {
    from,
    60%,
    75%,
    90%,
    to {
        -webkit-animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
        animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
    }

    from {
        opacity: 0;
        -webkit-transform: translate3d(0, 1000px, 0);
        transform: translate3d(0, 1000px, 0);
    }

    60% {
        opacity: 1;
        -webkit-transform: translate3d(0, -20px, 0);
        transform: translate3d(0, -20px, 0);
    }

    75% {
        -webkit-transform: translate3d(0, 10px, 0);
        transform: translate3d(0, 10px, 0);
    }

    90% {
        -webkit-transform: translate3d(0, -5px, 0);
        transform: translate3d(0, -5px, 0);
    }

    to {
        opacity: 1;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }
}

.bounceInUp {
    -webkit-animation: bounceInUp 0.8s;
    animation: bounceInUp 0.8s;
    /* animation-fill-mode : none | forwards | backwards | both;

值                 描述
none               不改变默认行为。
forwards           当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）。
backwards          在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。
both               向前和向后填充模式都被应用。 */
    animation-fill-mode: forwards;
}

@keyframes fadeInLeft {
    from {
        opacity: 0;
        -webkit-transform: translate3d(-100%, 0, 0);
        transform: translate3d(-100%, 0, 0);
    }
    to {
        opacity: 1;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }
}

.fadeInLeft {
    -webkit-animation: fadeInLeft 0.3s;
    animation: fadeInLeft 0.3s;
}

@keyframes fadeInRight {
    from {
        opacity: 0;
        -webkit-transform: translate3d(100%, 0, 0);
        transform: translate3d(100%, 0, 0);
    }
    to {
        opacity: 1;
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }
}

.fadeInRight {
    -webkit-animation: fadeInRight 0.3s;
    animation: fadeInRight 0.3s;
}

@keyframes fadeOutLeft {
    from {
        opacity: 1;
    }
    to {
        opacity: 0;
        -webkit-transform: translate3d(-100%, 0, 0);
        transform: translate3d(-100%, 0, 0);
    }
}

.fadeOutLeft {
    -webkit-animation: fadeOutLeft 0.5s;
    animation: fadeOutLeft 0.5s;
}

@keyframes fadeOutRight {
    from {
        opacity: 1;
    }
    to {
        opacity: 0;
        -webkit-transform: translate3d(100%, 0, 0);
        transform: translate3d(100%, 0, 0);
    }
}

.fadeOutRight {
    -webkit-animation: fadeOutRight 0.5s;
    animation: fadeOutRight 0.5s;
}

@keyframes bounceIn {
    from,
    20%,
    40%,
    60%,
    80%,
    to {
        -webkit-animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
        animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
    }
    0% {
        opacity: 0;
        -webkit-transform: scale3d(0.3, 0.3, 0.3);
        transform: scale3d(0.3, 0.3, 0.3);
    }
    20% {
        -webkit-transform: scale3d(1.1, 1.1, 1.1);
        transform: scale3d(1.1, 1.1, 1.1);
    }
    40% {
        -webkit-transform: scale3d(0.9, 0.9, 0.9);
        transform: scale3d(0.9, 0.9, 0.9);
    }
    60% {
        opacity: 1;
        -webkit-transform: scale3d(1.03, 1.03, 1.03);
        transform: scale3d(1.03, 1.03, 1.03);
    }
    80% {
        -webkit-transform: scale3d(0.97, 0.97, 0.97);
        transform: scale3d(0.97, 0.97, 0.97);
    }
    to {
        opacity: 1;
        -webkit-transform: scale3d(1, 1, 1);
        transform: scale3d(1, 1, 1);
    }
}

.bounceIn {
    -webkit-animation-duration: 0.75s;
    animation-duration: 0.75s;
    -webkit-animation-name: bounceIn;
    animation-name: bounceIn;
}

@keyframes bounceOutUp {
    20% {
        -webkit-transform: translate3d(0, -5px, 0);
        transform: translate3d(0, -5px, 0);
    }
    40%,
    45% {
        opacity: 1;
        -webkit-transform: translate3d(0, 20px, 0);
        transform: translate3d(0, 20px, 0);
    }
    to {
        opacity: 0;
        -webkit-transform: translate3d(0, -2000px, 0);
        transform: translate3d(0, -2000px, 0);
    }
}

.bounceOutUp {
    -webkit-animation: bounceOutUp 0.5s;
    animation: bounceOutUp 0.5s;
}

@keyframes nummove {
    /* 0% {
        margin-top: 50px
    }
    100% {
        margin-top: 0px
    } */
    0% {
        bottom: -50px;
    }
    100% {
        bottom: 0px;
    }
}

@keyframes linemove {
    0% {
        width: 0px;
    }
    100% {
        width: 100%;
    }
}

@keyframes namemove {
    0% {
        margin-right: 50px;
    }
    100% {
        margin-right: 0;
    }
}

@keyframes layer-border {
    0% {
        width: 0px;
        height: 0px;
    }
    100% {
        width: 100%;
        height: 100%;
    }
}

@media (min-width: 0px) {
    .demobg,
    .itembg {
        font-size: 14px;
    }
    .more {
        width: 30%;
    }
    .nomore,
    .more {
        font-size: 18px;
    }
    .item-num {
        font-size: 52px;
        line-height: 46px;
    }
    .item-name,
    .item-date {
        font-size: 14px;
        height: 24px;
        line-height: 24px;
    }
    #search .searchkey {
        width: calc(100% - 370px);
    }
    .searchresults {
        left: calc(2% + 350px);
    }
    .industryList {
        min-width: 200px;
    }
}

@media (min-width: 500px) {
    .demobg,
    .itembg {
        font-size: 24px;
    }
    .more {
        width: 14%;
    }
    .nomore,
    .more {
        font-size: 14px;
    }
    .item-num {
        font-size: 72px;
        line-height: 72px;
    }
    .item-name,
    .item-date {
        font-size: 18px;
        height: 32px;
        line-height: 32px;
    }
    .searchType > li {
        font-size: 16px;
    }
}

@media (min-width: 798px) {
    .demobg,
    .itembg {
        font-size: 20px;
    }
    .more {
        font-size: 18px;
    }
    .nomore,
    .more {
        font-size: 18px;
    }
    .item-name,
    .item-date {
        font-size: 18px;
    }
    .item-num {
        line-height: 65px;
        font-size: 72px;
    }
}

/* 中等屏幕（桌面显示器，大于等于 992px） */

@media (min-width: 992px) {
    .demobg,
    .itembg {
        font-size: 20px;
    }
    .item-name,
    .item-date {
        font-size: 18px;
    }
    .nomore,
    .more {
        font-size: 20px;
    }
    .more {
        width: 12%;
    }
    .item-num {
        font-size: 72px;
    }
    .searchType > li {
        font-size: 18px;
    }
}

@media (min-width: 1200px) {
    .demobg,
    .itembg {
        font-size: 20px;
    }
    .col-lg-3 {
        width: 33.33333333%;
    }
    .item-name,
    .item-date {
        font-size: 16px;
    }
    .item-num {
        font-size: 54px;
    }
}
@media (min-width: 1536px) {
    .demobg,
    .itembg {
        font-size: 24px;
    }
    .item-num {
        font-size: 72px;
    }
    .searchresults {
        left: calc(17% + 150px);
    }
    #search .searchkey {
        width: 74%;
    }
}

/* 大屏幕（大桌面显示器，大于等于 1200px） */

@media (min-width: 2160px) {
    .col-lg-3 {
        width: 25%;
    }
    .title {
        font-size: 48px;
    }
    .demobg,
    .itembg,
    .subtitle,
    .searchType > li {
        font-size: 24px;
    }
    .industryList {
        min-width: 270px;
    }
}
@media (min-width: 2560px) {
    .demobg,
    .itembg {
        font-size: 32px;
    }
    .col-lg-3 {
        width: 25%;
    }
    .item-num {
        font-size: 90px;
    }
    .item-name,
    .item-date {
        font-size: 26px;
        height: 40px;
        line-height: 40px;
    }
}
@media (min-width: 3840px) {
    .title {
        font-size: 56px;
    }
    .subtitle {
        font-size: 32px;
    }
    .item-num {
        font-size: 102px;
    }
}
@-webkit-keyframes move {
    0% {
        background-position: 0 0;
    }
    50% {
        background-position: 100% 0;
    }
}

@keyframes move {
    0% {
        background-position: 0 0;
    }
    50% {
        background-position: 100% 0;
    }
}
body {
    background-color: #17191c;
    overflow-x: hidden;
}
input {
    padding: 0;
    border: none;
}

.index-content {
    position: relative;
    z-index: 1;
}

a {
    text-decoration: none;
    color: #ffffff;
}

.check:hover {
    text-decoration: none;
    color: #ffffff;
}

hr {
    margin-top: 0px;
    margin-bottom: 0px;
    background-color: #707984;
    border: none;
    height: 1px;
}
ul li {
    list-style: none;
}

#content {
    position: relative;
    transition-property: filter;
    transition-duration: 1s;
    -webkit-transition-property: filter;
    -webkit-transition-duration: 1s;
    opacity: 1;
}

.col-xs-10 {
    width: 80.333333%;
}

.item {
    padding-right: 40px;
    padding-left: 40px;
    margin-top: 30px;
}

.rerow {
    margin: 0;
    height: 100%;
    font-size: 24px;
}

.title {
    color: #ffffff;
    margin-top: 75px;
    font-size: 48px;
}

.subtitle {
    color: #707984;
    margin-top: 32px;
}

.linefloat {
    float: left;
    margin-left: 15px;
}

.line {
    width: 110px;
    margin-top: 12px;
    height: 1.5px;
}

.item-title {
    transition: opacity 1s;
}

.item-row {
    margin: 50px 30px 0px 30px;
}

.item-num {
    color: #707984;
    position: relative;
    bottom: 0;
}

.square {
    cursor: pointer;
    overflow: hidden;
    /* height: 500px; */
}

.square .zoom {
    width: 100%;
    height: 100%;
    transition: transform 0.8s;
    position: relative;
}

.item-img {
    margin: 0 auto;
    width: 200%;
}

.thumbnail {
    width: 100%;
    /* height: 64%; */
    overflow: hidden;
    background: #101214;
    margin-bottom: 30px;
    border: 2px solid rgba(0, 0, 0, 0);
    border-radius: 10px;
    position: relative;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: Center;
    padding: 23px;
}

.zoom-hover {
    transform: scale(2.2, 2.2);
}

.square .foreground {
    background-color: rgba(255, 180, 120, 0.2);
    position: absolute;
    width: 100%;
    height: 100%;
    opacity: 0;
    transition: 0.5s ease;
    z-index: 3;
}

.border-color {
    border: 2px solid #ff7f00;
}

.foreground-hover {
    opacity: 0.6;
}

.item-introduce {
    height: 130px;
}

.item-name,
.item-date {
    color: #707984;
}

.white-color {
    color: #ffffff;
}

.black-color {
    color: #000000;
}

.white-bgcolor {
    background: #ffffff;
}

.nummove {
    animation: nummove 0.5s;
}

.linemove {
    animation: linemove 0.5s;
}

.namemove {
    animation: namemove 0.5s;
}

.layer-border {
    animation: layer-border 0.5s;
}

.layer {
    position: absolute;
    margin: 0;
    border: 3px solid #000000;
    width: 100%;
    height: 100%;
    font-size: 30px;
    opacity: 0;
    transition: 0.5s ease;
    overflow: hidden;
    top: 0;
    left: 0;
}

.layer-show {
    opacity: 1;
}

.layer-hide {
    opacity: 0;
}
.layerbtn {
    width: 100%;
    height: 23%;
    position: absolute;
    top: 50%;
    width: 100%;
    transform: translateY(-50%);
}
.demobg {
    position: absolute;
    left: 0px;
    height: 100%;
    background-color: rgba(16, 18, 20, 0.8);
    background-size: 100%;
}

.itembg {
    position: absolute;
    right: 0px;
    height: 100%;
    margin-left: -14%;
    background-color: rgba(16, 18, 20, 0.8);
    background-size: 100%;
}
.itembg p,
.demobg p {
    /* vertical-align: middle;
    display: table-cell; */
    display: flex;
    justify-content: center;
    align-items: Center;
    height: 100%;
}
.itembg:hover,
.demobg:hover {
    background-color: rgba(255, 127, 0, 0.8);
}

.morebtn {
    position: absolute;
    width: 100%;
    height: 3%;
    z-index: 4;
    margin-top: 50px;
}

.more {
    margin: 0 auto;
    text-align: center;
    border-radius: 10px;
    cursor: pointer;
    color: #707984;
    background: #2b2e32;
    padding: 8px 20px 8px 20px;
}

.more:hover {
    background: rgba(255, 127, 0, 0.8);
    color: #ffffff;
}

.nomore {
    text-align: center;
    width: 100%;
    color: #707984;
    display: none;
}

.totop {
    position: absolute;
    width: 84px;
    height: 84px;
    z-index: 5;
    cursor: pointer;
    background: url(/static/img/totop.png) no-repeat;
    bottom: -290px;
    left: 50%;
    transform: translate(-50%);
}

.totop:hover {
    background: url(/static/img/totop1.png) no-repeat;
}

.totop a {
    display: block;
    height: 84px;
    width: 84px;
}

#model {
    transition-property: right;
    transition-duration: 1s;
    -webkit-transition-property: right;
    -webkit-transition-duration: 1s;
    /* position: absolute; */
    right: -100%;
    top: 0;
    opacity: 1;
    z-index: 100000;
}

.overflow {
    width: 100%;
    height: 100%;
    overflow: hidden;
    position: relative;
}

.searchType {
    width: 100%;
    margin: 0;
    padding: 0px 70px;
    height: 70px;
}

.searchType > li {
    float: left;
    color: #727c8d;

    width: 5%;
    cursor: pointer;
    border-bottom: 1px solid rgba(0, 0, 0, 0);
    background-position: 95% 50%;
    background-repeat: no-repeat;
    line-height: 70px;
    min-width: 72px;
    /* 禁止复制 */
    -webkit-user-select: none;
    user-select: none;
}
.data-search-industry {
    position: relative;
}

.industryList {
    position: absolute;
    top: 71px;
    padding: 0;
    z-index: 10;
    /* background: hsla(0,0%,100%,0.1); */
    background: rgb(23, 25, 28, 0.75);
    border-radius: 0 0 10px 10px;
    width: 100%;
    display: none;
    cursor: pointer;
}
.industryList > li {
    text-align: left;
    line-height: 50px;
    padding: 0 32%;
    color: rgba(255, 255, 255, 0.8);
}
#search {
    margin-top: 50px;
}
#search .searchbtn {
    width: 5%;
}
#search .bgline {
    height: 1px;
    padding: 0px 70px;
    background-color: #707984;
    background-clip: content-box; /*只有内容设置背景 */
}

.search {
    background: url('/static/img/search.png') no-repeat;
    width: 23px;
    height: 23px;
    float: left;
    padding-left: 50px;
}
#searchValue {
    background: rgba(0, 0, 0, 0);
    outline: none;
    width: 80%;
    margin-left: 50px;
}
.searchBox {
    padding-left: 5%;
    visibility: hidden;
    background: url(/static/img/search.png) no-repeat 5%;
}
/* .data-search-industry.hover, .data-search-name:hover, .data-search-industry:hover {
  border-bottom: 1px solid #ffffff;
} */
.li-move {
    transition: all 0.3s ease-in-out;
}
#search .descSort {
    background-image: url('/static/img/desc.png');
}

#search .ascSort {
    background-image: url('/static/img/asc.png');
}
#search .removeSort {
    background-image: none;
    border-bottom: 1px solid rgba(0, 0, 0, 0);
}
.searchresultsbox {
    position: relative;
    width: 100%;
}
.searchresults {
    position: absolute;
    width: 60%;
    /* left: 21%; */
    right: 0;
    /* background: #fff; */
    font-size: 18px;
    z-index: 5;
    border-radius: 0 0 10px 10px;
    visibility: hidden;
    background: hsla(0, 0%, 100%, 0.15);
    /* background: rgb(23, 25, 28,0.75); */
}
.searchresults h3 {
    color: #4c5460;
    font-size: 18px;
    margin-left: 60px;
}
.searchresults-section {
    box-sizing: content-box;
}
.searchresults-list {
    color: #727c8d;
    padding: 0;
}

.searchresults-list li {
    cursor: pointer;
    line-height: 36px;
    padding: 0px 96px;
}
.searchresults-list li:hover,
.industryList > li:hover,
.user-info-box li:hover {
    background: #ff7f00;
    color: #ffffff;
}

.filter {
    -webkit-filter: blur(26px);
    filter: blur(26px);
    transition-property: filter;
    transition-duration: 0.5s;
    -webkit-transition-property: filter;
    -webkit-transition-duration: 0.5s;
}
/* 禁用点击 */
.disable {
    pointer-events: none;
}
#curtain {
    display: none;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 9998;
}
</style>