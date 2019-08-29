<template>
    <!-- 首页 -->
    <div v-if="isShow" :class="['home-page',isLogin ? 'blur' : '']" id="header">
        <div style="position:absolute;width: 100%;height: 99.6vh;">
            <video
                autoplay="autoplay"
                loop="loop"
                muted="true"
                style="width:100%;height:100%;object-fit:fill;"
            >
                <source src="static/img/home.mp4" type="video/mp4" />
            </video>
        </div>
        <div class="container-fluid header-content">
            <div class="row">
                <div class="col-sm-12 earth img-responsive">
                    <div class="word1">
                        <span style="letter-spacing:8px;">优锘科技数据可视化案例</span>
                    </div>
                    <div class="word2">
                        <span style="letter-spacing:4px;">致力实现人性、智能、众创的可视化</span>
                    </div>
                    <div class="word3 check" :style="{visibility: isLogin ? 'hidden' : 'visible'}" @click="checkLogin">
                        <span style="letter-spacing:2px;">立即体验</span>
                    </div>
                </div>
            </div>
        </div>
        <div class="container-fluid middle-content">
            <div class="col-sm-3 middle middle1">
                <div class="photo">
                    <div class="photo-word">效率</div>
                    <img
                        src="static/img/circle.png"
                        class="img-responsive photo-img"
                        alt="Responsive image"
                    />
                </div>
                <div class="bottom-word">
                    <p>
                        快速搭建可视化大屏，在保证
                        <br />质量的同时大幅提升交付速度
                    </p>
                </div>
            </div>
            <div class="col-sm-3 middle middle2">
                <div class="photo">
                    <div class="photo-word">专业</div>
                    <img
                        src="static/img/circle.png"
                        class="img-responsive photo-img"
                        alt="Responsive image"
                    />
                </div>
                <div class="bottom-word">
                    <p>
                        沉淀多年行业经验，为每一
                        <br />位客户量身定制可视化场景
                    </p>
                </div>
            </div>
            <div class="col-sm-3 middle middle3">
                <div class="photo">
                    <div class="photo-word">敏捷</div>
                    <img
                        src="static/img/circle.png"
                        class="img-responsive photo-img"
                        alt="Responsive image"
                    />
                </div>
                <div class="bottom-word">
                    <p>
                        <span style="letter-spacing: 1.2px;">从样式、组件、模板、动效层</span>
                        <br />层迭代，建立可视化的系统生态
                    </p>
                </div>
            </div>
            <div class="col-sm-3 middle middle4">
                <div class="photo">
                    <div class="photo-word">价值</div>
                    <img
                        src="static/img/circle.png"
                        class="img-responsive photo-img"
                        alt="Responsive image"
                    />
                </div>
                <div class="bottom-word">
                    <p>
                        帮助客户理解数据，使数据产生知
                        <br />识，辅助决策，提升客户管理水平
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: ['Home'],
    data() {
        return {
            isLogin: false,
            isShow: true,
        };
    },
    methods: {
        checkLogin() {
            this.$emit('home')
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
