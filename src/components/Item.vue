<template>
    <div
        class="col-xs-12 col-sm-6 col-md-6 col-lg-3 item bounceInUp"
        :style="{opacity: 0, animationDelay: 0.1 * (index - start) + 's' }"
    >
        <div class="square" @mouseenter="itemMouseenter" @mouseleave="itemMouseleave">
            <!-- 项目缩略图 -->
            <div :class="['thumbnail',itemMouse ? 'border-color' : '']">
                <div class="overflow">
                    <div :class="['zoom', itemMouse ? 'zoom-hover' : '']">
                        <div class="foreground" :style="{opacity: itemMouse ? 1 : 0}"></div>
                        <img
                            :src="item.list.thumbUrl"
                            class="img-responsive item-img"
                            :alt="item.list.name"
                        />
                    </div>
                    <!-- 浮层显示项目选项 -->
                    <div :class="['row','layer', itemMouse ? 'layer-show' : 'layer-hide']">
                        <div class="layerbtn">
                            <div class="col-xs-6 text-center white-color demobg" :class="itemMouse ? 'fadeInLeft' : 'fadeOutLeft'">
                                <p>查看DEMO</p>
                            </div>
                            <div class="col-xs-6 text-center white-color itembg" :class="itemMouse ? 'fadeInRight' : 'fadeOutRight'">
                                <p>项目详情</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- 项目简介 -->
            <div class="row item-introduce">
                <div
                    :class="['col-xs-2', 'item-num', 'text-left',itemMouse ? ['white-color','nummove'] : '']"
                >{{ index < 9 ? '0' + (index+1) : (index+1)}}</div>
                <div class="col-xs-10">
                    <div
                        :class="['text-right', 'item-name', itemMouse ? ['white-color', 'namemove']  : '']"
                    >{{item.list.name}}</div>
                    <hr :class="['item-line', itemMouse? ['white-bgcolor','linemove'] : '']" />
                    <div
                        :class="['text-right', 'item-date', itemMouse ? ['white-color', 'namemove'] : '']"
                    >{{item.list.date}}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: {
        item: Object,
        index: Number,
    },
    data() {
        return {
            showData: [],
            start: 0, //加载从第几条
            itemMouse: false,
            currData: [],
        };
    },
    created() {
        this.$http.get('/static/json/mock.json').then(data => {
            this.currData = [...data.data];
            this.showData = this.currData.slice(0, 6);
        });
    },
    methods: {
        itemMouseenter() {
            this.itemMouse = true;
        },
        itemMouseleave() {
            this.itemMouse = false;
        },
    },
};
</script>

<style scoped>
</style>
