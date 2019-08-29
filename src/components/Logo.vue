<template>
    <!-- 首页 -->
    <div id="logo">
        <div v-if="isLogin || isShow" id="main_logo" class="col-sm-1 company-logo" style="z-index:10000;">
            <img
                src="/static/img/logo.png"
                class="img-responsive uinnova-logo"
                @click="goUinnova"
                alt="logo"
            />
        </div>
        <div class="col-sm-1 col-sm-offset-8 common-logo hidden-logo" id="user-logo">
            <img @click="showUserInfo"
                src="/static/img/user1.png"
                class="img-responsive right-icon-img people-logo"
                alt="logo"
            />
            <div v-show="isShowUserInfo"
                class="popover fade bottom in user-info-box"
                id="user-info-box"
                role="tooltip"
                style="top: 28px;"
            >
                <div class="arrow" style="left: 23.4601%;"></div>
                <div class="popover-content">
                    <ul style="margin-bottom: 0;">
                        <li id="loginout" onclick="loginOut()">切换账号</li>
                        <li
                            id="loginout"
                            onclick="loginOut()"
                            style="border-radius: 0 0 10px 10px;"
                        >退出登陆</li>
                    </ul>
                </div>
            </div>
        </div>
        <div v-if="!isShow" class="col-sm-1 common-logo hidden-logo" id="goindex-logo" @click="goHome">
            <img src="/static/img/goindex.png" class="img-responsive right-icon-img" alt="logo" />
        </div>
        <div class="col-sm-1 common-logo right-icon" id="qrcode">
            <img
                src="static/img/right_icon.png"
                id="erweima"
                @click="showQRCode"
                class="img-responsive right-icon-img"
                alt="right-icon"
            />
            <img
                src="static/img/right-uinnova.png"
                id="ma"
                :class="['img-responsive', 'right-uinnova',codeActive ? 'right-uinnova-active' : '']"
                alt="right-uinnova"
            />
        </div>
    </div>
</template>

<script>
export default {
    name: 'Home',
    props: ['Home'],
    data() {
        return {
            isLogin: true,
            isShow: false,
            isShowUserInfo: false,
            codeActive: false,
        };
    },
    methods: {
        //左侧uinnova图标
        goUinnova() {
            window.open('http://www.uinnova.cn/');
        },
        //展示二维码
        showQRCode() {
            this.codeActive = !this.codeActive;
        },
        //返回首页
        goHome() {
            this.isShow = true
            this.$emit('home', { param: true });
        },
        //展示用户功能
        showUserInfo() {
            this.isShowUserInfo = true;
        }    
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
/* 首页介绍圆圈适配 */
@media (min-width: 2790px) {
    .photo-img {
        width: 70%;
    }
}
/*去除自带的默认样式*/

body {
    padding: 0;
    margin: 0;
    font-family: 'Helvetica Neue For Number', -apple-system, BlinkMacSystemFont,
        'Segoe UI', Roboto, 'Hiragino Sans GB', 'Microsoft YaHei', 'PingFang SC',
        'Helvetica Neue', Helvetica, Arial, sans-serif;
    /* overflow: hidden; */
}

.uinnova-logo::selection {
    background: #ff7f00;
    color: #fff;
}

.word1-span::selection {
    background: #ff7f00;
    color: #fff;
}

.home-page {
    background-image: url(/static/img/home.png);
    background-repeat: no-repeat;
    background-size: 100%;
    height: 100vh;
}

.right-icon-img {
    cursor: pointer;
    float: right;
}

#logo {
    display: block;
    position: absolute;
    width: 100%;
    top: 0;
    padding: 50px 50px;
    transition: opacity 0.5s;
}
#logo .company-logo {
    width: 8.4vw;
    top: 50%;
    transform: translateY(-50%);
}
#logo .common-logo {
    width: 4%;
    top: 50%;
    transform: translateY(-50%);
    z-index: 2;
}
.user-info-box {
    top: 30px;
    color: #ffffff;
    font-size: 0.7vw;
    top: 34px;
    padding: 0;
    z-index: 10;
    background: hsla(0, 0%, 100%, 0.1);
    width: 100%;
    min-width: 140px;
    cursor: pointer;
    left: unset;
}
.user-info-box ul {
    padding: 0;
}
.user-info-box li {
    text-align: center;
    line-height: 50px;
    color: #727c8d;
}
.popover.bottom > .arrow:after {
    border-bottom-color: hsla(0, 0%, 100%, 0.1);
}
.popover-content {
    padding: 0;
}
.col-sm-offset-8 {
    margin-left: calc(88% - 8.4vw);
}
.uinnova-logo {
    cursor: pointer;
}

.right-icon {
    z-index: 2;
}

.right-uinnova {
    position: absolute;
    right: 50%;
    top: 100%;
    display: none;
}

.right-uinnova-active {
    display: inline;
    min-width: 200%;
}
.earth {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: justify;
    /* margin-top: -40px; */
}

.word1 {
    position: absolute;
    top: 40%;
    color: white;
    font-size: 3.1vw;
}

.word2 {
    position: absolute;
    top: 55%;
    color: white;
    font-size: 1.2vw;
}

.word3 {
    position: absolute;
    top: 66%;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: justify;
    width: 12.5vw;
    height: 5.6vh;
    /* border: 2px solid #ff7f00; */
    background-color: #ff7f00;
    border-radius: 10px;
    cursor: pointer;
    color: white;
    font-size: 1.4vw;
}

.middle-content {
    width: auto;
    height: 325px;
}

.middle {
    height: 325px;
    position: relative;
    display: flex;
    justify-content: center;
}

.photo {
    width: 26%;
    height: 37%;
    position: absolute;
    top: 80px;
    /* background: url(/static/img/circle.png) no-repeat; */
    background-size: 100% 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: justify;
}

.photo-word {
    color: rgba(255, 255, 255, 1);
    font-size: 1.6vw;
    position: absolute;
}

.bottom-word {
    font-size: 0.8vw;
    position: absolute;
    top: 233px;
    font-weight: bold;
    color: rgba(112, 121, 132, 1);
}

.footer-box {
    width: 100%;
    height: 16vh;
    position: relative;
    background-color: rgba(16, 18, 20, 1);
    margin-top: 250px;
    min-height: 200px;
    padding: 0 100px;
    bottom: 0;
}

.footer1,
.footer2,
.footer3,
.footer4 {
    display: flex;
    justify-content: center;
    height: 16vh;
    padding-top: 50px;
    padding-bottom: 50px;
    align-items: center;
    min-height: 200px;
    line-height: 16vh;
}

.footer1 {
    line-height: normal;
}
.uin-word1 {
    font-size: 1.2vw;
    color: #707984;
    cursor: pointer;
    position: absolute;
    top: 40px;
}
.uin-word1:hover {
    color: #ff7f00;
}
.uin-word2 {
    font-size: 0.8vw;
    color: #707984;
    display: block;
    /* position: relative;
    top: 50px; */
}
.footer2,
.footer3,
.footer4 {
    font-size: 0.8vw;
    color: #707984;
}

/*设置滚动条样式*/

body::-webkit-scrollbar {
    width: 5px;
    height: 10px;
}

body1::-webkit-scrollbar-thumb {
    border-radius: 100px;
}

body::-webkit-scrollbar-button {
    height: 0;
}

body::-webkit-scrollbar-track {
    background: rgba(1, 41, 82, 0.3);
    border-radius: 1px;
}

body::-webkit-scrollbar-thumb {
    background: #00c7ff;
    border-radius: 1px;
}

body::-webkit-scrollbar-corner {
    background: #00c7ff;
}

@media screen and (max-width: 767px) {
    .header-content {
        background-color: white;
    }
}

@media screen and (min-width: 0) {
    .header-content {
        height: 66vh;
    }
    .earth {
        height: 62vh;
    }
    .middle-content {
        height: 30vh;
    }
}

/* 登陆样式 */

#login {
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    /* display: none; */
    /* background-color: rgba(0, 0, 0, 0.6); */
    z-index: 100;
}

@keyframes changebox {
    0% {
        top: -14%;
    }
    100% {
        top: 14%;
    }
}

#loginbox {
    background: url('/static/img/login.png') no-repeat 0 0;
    height: 63vh;
    width: 31.6vw;
    background-size: 100% 100%;
    -moz-background-size: 100% 100%;
    position: relative;
    margin: auto;
    top: 14vh;
    z-index: 105;
    /* -webkit-transition: transform 0.8s;
    -o-transition: transform 0.8s;
    transition: transform 0.8s; */
}

.forma {
    /* -webkit-transform: translateY(-700px);
    -ms-transform: translateY(-700px);
    -o-transform: translateY(-700px);
    transform: translateY(-700px); */
    animation: changebox 0.5s linear 1;
}

#login_form {
    position: relative;
    top: 23.1vh;
}

#logintext {
    font-size: 1.5vh;
    letter-spacing: 2px;
    font-weight: 400;
    font-family: Microsoft YaHei;
}

.loginlabel {
    font-weight: 400;
    margin-left: -1.3vh;
    color: rgba(255, 255, 255, 0.6);
}

.forgetpassword {
    float: right;
    color: rgb(255, 255, 255);
    padding-top: 7px;
    padding-bottom: 0px;
    border-bottom: 1px solid #333;
    cursor: pointer;
}

input[type='checkbox'] {
    width: 0.83vw;
    height: 0.83vw;
    display: inline-block;
    text-align: center;
    vertical-align: middle;
    line-height: 0.83vw;
    border-radius: 3px 3px;
    position: relative;
    margin: 0;
    background-color: #395573;
}

input[type='checkbox']::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    background-color: #395573;
    width: 100%;
    height: 100%;
    cursor: pointer;
}

input[type='checkbox']:checked::before {
    content: '\2713';
    background-color: #395573;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    color: #fff;
    font-size: 1.3vh;
    font-weight: bold;
    cursor: pointer;
}

#usericon {
    background: url('/static/img/user.png') no-repeat 0.52vw;
    padding-left: 2.1vw;
    border: 0;
    background-color: rgba(114, 124, 141, 0.3);
    font-size: 1.5vh;
    padding-top: 12px;
    font-family: Microsoft YaHei;
    -moz-background-size: 2.13vh;
    background-size: 2.13vh;
    color: rgba(255, 255, 255, 1);
}

#passwordicon {
    background: url('/static/img/password.png') no-repeat 0.52vw;
    padding-left: 2.1vw;
    border: 0;
    background-color: rgba(114, 124, 141, 0.3);
    padding-top: 1.3ch;
    font-size: 1.5vh;
    font-family: Microsoft YaHei;
    -moz-background-size: 2.13vh;
    background-size: 2.13vh;
    color: rgba(255, 255, 255, 1);
}

.btnsubmit {
    width: 100%;
    border: 0;
    background-color: #ff7f00;
    border-radius: 5px;
    color: rgb(255, 255, 255);
    font-size: 2.34vh;
}

.btnsubmit:hover {
    color: rgb(255, 255, 255);
}

.btnsubmit:focus {
    color: rgb(255, 255, 255);
    outline: none !important;
}

.top-buffer {
    margin-top: 2vh;
}

.top-buffer1 {
    margin-top: 2.8vh;
}

.form-control {
    line-height: 7.94vh;
    height: 4.6vh;
}

.blur {
    -webkit-filter: blur(20px);
    /* Chrome, Safari, Opera */
    filter: blur(20px);
    /* transform: scale(1.2);
    -ms-transform: scale(1.2);
    -moz-transform: scale(1.2);
    -webkit-transform: scale(1.2);
    -o-transform: scale(1.2); */
}

.form-control:focus {
    -webkit-box-shadow: none;
    box-shadow: none;
}
#login .login-close-box {
    cursor: pointer;
    right: 1.5%;
}
</style>
