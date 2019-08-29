<template>
     <!-- 项目详情弹框部分 -->
        <div class="wrap" id="model">
            <header class="popup-head" id="head">
                <div class="popup-logo">
                    <img src="static/img/popup_logo.png">
                </div>
                <div class="popup-title">
                    <span class="project-title">可视化项目</span>
                </div>
                <div class="close-button" id="closed">
                    <div class="close-box">
                        <img src="static/img/close.png" width="24px" height="24px">
                    </div>
                </div>
            </header>
            <section class="popup-content">
                <div class="popup-img-carousel">
                    <div class="list">
                        <ul class="list-ul">

                        </ul>
                    </div>

                    <div class="buttons">

                    </div>
                </div>
                <div class="popup-arrow">
                    <a href="javascript:;" class="prev popup-btn-left">
                        <img src="static/img/arrow-left.png">
                    </a>
                    <a href="javascript:;" class="next popup-btn-right">
                        <img src="static/img/arrow-right.png">
                    </a>
                </div>
            </section>
            <!-- <div>
                <a href="#project" id="goDown" class="probtn"></a>
                <a href="#head" id="goUp" class="probtn"></a>
            </div> -->
            <div class="info" id="project">
                <div class="popup-project">
                    <div class="popup-project-common popup-project1"></div>
                    <div class="popup-project2"><a href="#item-infor">项目详情</a></div>
                    <div class="popup-project-common popup-project3"></div>
                    <div class="popup-project5">项目看板</div>
                    <div class="popup-project-common popup-project6"></div>
                </div>
                <div class="popup-project4"></div>
                <table id="item-infor" border="0" style="width: 65%;margin: 5vh auto 0 auto;">
                    <tr>
                        <td align="left" width="25%" class="info-title">客户名称</td>
                        <td align="left" class="customer-name"></td>
                    </tr>
                    <tr>
                        <td align="left" class="info-title">项目介绍</td>
                        <td align="left" class="intro"></td>
                    </tr>
                    <tr>
                        <td align="left" class="info-title">主题内容</td>
                        <td align="left" class="category"></td>
                    </tr>
                    <tr>
                        <td align="left" class="info-title">客户环境</td>
                        <td align="left" class="env"></td>
                    </tr>
                    <tr>
                        <td align="left" class="info-title">所属行业</td>
                        <td align="left" class="industry"></td>
                    </tr>
                </table>
            </div>
        </div>
</template>

<script>
export default {
  name: 'Detail',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.close-box:hover {
    -webkit-transform: rotate(180deg);
    transform: rotate(180deg);
}


/*去除自带的默认样式*/

body {
    padding: 0;
    margin: 0;
    /* background-color:#000000; */
}

.wrap {
    width: 100%;
    height: 100%;
    position: fixed;
    /* display: none; */
    float: left;
    top: 0;
    z-index: 100000;
    overflow-y: auto;
    overflow-x: hidden;
    /* background-image: url(/static/img/layout.png);
    background-repeat: no-repeat;
    background-size: 100% 100%; */
}


/* 列表页的头部 */

#content-head-wu {
    width: 100%;
    /* position: absolute;
    top: 0px; */
    height: 9vh;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    /* border-bottom: 1px solid rgba(255, 255, 255, 0.1); */
    z-index: 9999;
    background: rgba(23, 25, 28, 0.5);
}

.content-head-logo {
    width: 10%;
}

.content-popup-title {
    width: 90%;
    text-align: right;
    color: #ffffff;
    font-size: 18px;
    cursor: pointer;
    height: 30px;
    line-height: 30px;
    background: url(/static/img/goindex.png) no-repeat;
    background-position: right;
}
.content-popup-title span:hover {
    border-bottom: 1px solid #ffffff;
    display: inline;
    line-height: 30px;
    display: inline-block;
}

.content-head-right-icon {
    width: 5%;
}

.content-right-icon-img {
    cursor: pointer;
}

.content-right-uinnova {
    position: absolute;
    right: 49px;
    top: 54px;
    display: none;
}

.content-dis {
    display: inline;
}

.content-head-right-box {
    position: absolute;
    right: 0px;
    top: 0px;
    width: 8vh;
    height: 9vh;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
}

.item-title {
    padding-top: 12px;
}

.popup-logo {
    width: 10%;
}

.popup-title {
    width: 80%;
}

.close-button {
    width: 10%;
}

.popup-head {
    position: absolute;
    top: -10%;
    width: 100%;
    height: 9vh;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    font-size: 1.2vw;
    color: white;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}
.popup-head-ani{
    animation: po-head 0.5s linear;
    animation-delay:1.57s;
    animation-fill-mode: forwards;
} 
@keyframes po-head{
    from {
        top: -10%;
    }
    to {
        top: 0;
    }
}
.close-box {
    position: absolute;
    right: 0px;
    top: 0px;
    width: 7vh;
    height: 9vh;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    z-index: 100000;
    -webkit-transition: -webkit-transform 0.5s ease-out;
    -moz-transition: -moz-transform 0.5s ease-out;
    -o-transition: -o-transform 0.5s ease-out;
    -ms-transition: -ms-transform 0.5s ease-out;
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
}

.popup-content {
    position: relative;
    top: 7vh;
    width: 100%;
    height: 91vh;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
}

.popup-img-carousel {
    width: 90%;
    margin-top: 2vh;
    /* height: 86vh; */
    position: relative;
}


/* .list{
    width: 100%;
	max-height: 82vh;
	overflow: hidden;
	position: absolute;
	/* left: 50%;
	margin-left: -600px; 
} */

.list-ul {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    max-height: 70vh;
    padding: 0;
}

.list-ul li {
    border: 15px solid;
    border-radius: 10px;
    border-top-color: rgba(255, 255, 255, 0.2);
    border-left-color: rgba(255, 255, 255, 0.2);
    border-bottom-color: rgba(255, 255, 255, 0.2);
    border-right-color: rgba(255, 255, 255, 0.2);
    /* position: absolute; 
    opacity: 0;  */
    list-style: none;
    transition: all 1s ease;
    width: 70%;
}

.imag-pop {
    border: 1px solid rgba(0, 0, 0, 1);
    max-height: 78vh;
}

.p0 {
    position: absolute;
    transform: translate3d(-1140px, 0, 0) scale(0.5);
    opacity: 0.8;
    z-index: 2;
}

.p0-ani{
    animation: p0-ani 5s linear;
    animation-delay:1s;
    animation-fill-mode: forwards;
}

/* @keyframes p0-ani {
    from {
        transform: translate3d(-1800px, 0, 0) scale(0.5);
    }
    to {
        transform: translate3d(-1340px, 0, 0) scale(0.5);
    }
  } */

.p1 {
    opacity: 1;
    z-index: 50;
}

.p2 {
    position: absolute;
    transform: translate3d(1140px, 0, 0) scale(0.5);
    opacity: 0.8;
    z-index: 1;
}

/* .p2-ani{
    animation: p22-ani 0.5s linear;
    animation-delay:1s;
    animation-fill-mode: forwards;
}

@keyframes p22-ani {
    from {
        right: 0%;
    }
    to {
        right: 20%;
    }
  } */

.p3 {
    position: absolute;
    transform: translate3d(2480px, 0, 0) scale(0.5);
    opacity: 0.8;
    z-index: 3;
}

.p4 {
    position: absolute;
    transform: translate3d(3720px, 0, 0) scale(0.5);
    opacity: 0.8;
    z-index: 4;
}

.p5 {
    position: absolute;
    transform: translate3d(4860px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.p6 {
    position: absolute;
    transform: translate3d(6000px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.p7 {
    position: absolute;
    transform: translate3d(7000px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.p8 {
    position: absolute;
    transform: translate3d(8000px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.p9 {
    position: absolute;
    transform: translate3d(9000px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.p10 {
    position: absolute;
    transform: translate3d(10000px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.p11 {
    position: absolute;
    transform: translate3d(11000px, 0, 0) scale(0.5);
    opacity: 0.8;
}

.popup-arrow {
    position: absolute;
    width: 100%;
    top: 43%;
    z-index: 99;
    left: 0;
}

.popup-btn-left {
    position: absolute;
    left: 50px;
    opacity: 0;
}

.popup-btn-right {
    position: absolute;
    right: 50px;
    opacity: 0;
}

.popup-btn-left-ani{
    animation: popup-btn-left-ani 1s linear;
    animation-delay:2s;
    animation-fill-mode: forwards;
}

@keyframes popup-btn-left-ani {
    from {
        opacity: 0;
        left: 50px;
    }
    to {
        opacity: 1;
        left: 20px;
    }
  }

  .popup-btn-right-ani{
    animation: popup-btn-right-ani 1s linear;
    animation-delay:2s;
    animation-fill-mode: forwards;
}

@keyframes popup-btn-right-ani {
    from {
        opacity: 0;
        right: 50px;
    }
    to {
        opacity: 1;
        right: 20px;
    }
  }


/* .popup-btn-left{
    display: flex;
    align-items: left;
    justify-content: left;
    text-align: left;
} */

.buttons {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
}

.buttons span {
    height: 10px;
    margin: 18px 5px 20px;
    border-radius: 5px;
    transition: width .3s ease, background .3s ease;
}

.pop-btn {
    width: 10px;
    background: hsla(0, 0%, 100%, .3);
    cursor: pointer;
    opacity: 0;
}

.pop-btn-ani{
    animation: pop-btn-ani 2s linear;
    animation-delay:2s;
    animation-fill-mode: forwards;
}

@keyframes pop-btn-ani {
    0% {
        opacity: 0;
    }
    20%{
        opacity: 0.2;
    }
    40%{
        opacity: 0.4;
    }
    60%{
        opacity: 0.6;
    }
    80%{
        opacity: 0.8;
    }
    100% {
        opacity: 1;
    }
  }


.active {
    width: 25px;
    /* background: #d8d8d8; */
    background: hsla(0, 0%, 100%, .3);
    cursor: default;
}

.info {
    position: absolute;
    top: -100%;
    height: 67vh;
    z-index: 9000000000;
    width: 100%;
}

.info-ani{
    animation: pop-info 0.5s linear;
    animation-delay:2s;
    animation-fill-mode: forwards;
}

@keyframes pop-info {
    from {
        top: 100%;
    }
    to {
        top: 90vh;
    }
  }

tr {
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    color: #707984;
    width: 100%;
}

td {
    font-size: 1.2vw;
    padding: 17px;
}

.popup-project {
    display: flex;
    align-items: center;
    width: 100%;
}

.popup-project1 {
    width: 18%;
}

.popup-project4 {
    display: inline-block;
    width: 11.2%;
}

.popup-project2 {
    display: inline-block;
    font-size: 1.2vw;
    width: 7%;
    text-align: left;
    color: white;
    background: url(/static/img/downshow.png) no-repeat;
    background-position: 93% 57%;
    padding-left: 0.5%;
    background-size: 1vw;
    cursor: pointer;
}
.popup-project2 a:hover,.popup-project2 a:visited,.popup-project2 a:link,.popup-project2 a:active {
    text-decoration: none;
    color: #ffffff;
}
.popup-project3 {
    width: 50%;
}
.popup-project5 {
    display: inline-block;
    font-size: 1.2vw;
    width: 7%;
    text-align: right;
    color: #ffffff;
    background: url(/static/img/itemlink.png) no-repeat;
    background-position: 7% 57%;
    background-size: 1vw;
    padding-right: 0.5%;
    cursor: pointer;
}
.popup-project6 {
    width: 18%;
    
}

.popup-project-common {
    height: 1px;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    display: inline-block;
}


/* 查看详情 */

.probtn {
    position: absolute;
    bottom: 70px;
    right: 20px;
    width: 84px;
    height: 84px;
}

#goDown {
    background: url(/static/img/down.png) no-repeat;
}

#goUp {
    background: url(/static/img/totop.png) no-repeat;
}

#goDown {
    width: 84px;
    height: 84px;
    display: block;
    padding: 8px;
}


/*设置弹出框条样式*/

.wrap::-webkit-scrollbar {
    width: 0px;
    height: 10px;
}

.wrap1::-webkit-scrollbar-thumb {
    border-radius: 100px;
}

.wrap::-webkit-scrollbar-button {
    height: 0;
}

.wrap::-webkit-scrollbar-track {
    background: rgba(1, 41, 82, 0.3);
    border-radius: 1px;
}

.wrap::-webkit-scrollbar-thumb {
    background: #474646;
    border-radius: 1px;
}

.wrap::-webkit-scrollbar-corner {
    background: #474646;
}


/*设置滚动条样式*/

body::-webkit-scrollbar {
    width: 0px;
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
    background: #474646;
    border-radius: 1px;
}

body::-webkit-scrollbar-corner {
    background: #474646;
}
</style>
