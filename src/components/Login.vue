<template>
    <!-- 登陆部分 -->
    <div v-if="isLogin" id="login">
        <div class="close-box login-close-box" @click="loginClose">
            <img src="/static/img/close.png" width="24px" height="24px" />
        </div>

        <div :class="['form', 'row', isLogin ? 'forma' : '']" id="loginbox">
            <form
                class="form-horizontal col-sm-offset-2 col-md-offset-2"
                id="login_form"
                name="addForm"
                @submit="checkSubmit"
            >
                <div class="col-sm-9 col-md-9">
                    <div class="form-group top-buffer1">
                        <i class="fa fa-user fa-2x fa-lg"></i>
                        <input
                            id="usericon"
                            class="form-control required"
                            type="text"
                            placeholder="Username"
                            name="username"
                            autofocus="autofocus"
                            autocomplete="off"
                            maxlength="20"
                            ref="username"
                        />
                    </div>
                    <div class="form-group top-buffer">
                        <i class="fa fa-lock fa-2x fa-lg"></i>
                        <input
                            id="passwordicon"
                            class="form-control required"
                            type="password"
                            placeholder="Password"
                            name="password"
                            ref="password"
                        />
                    </div>
                    <div class="form-group top-buffer1">
                        <input
                            type="submit"
                            class="btn btnsubmit"
                            :style="border = isLogin ? 'none' : ''"
                            value="登陆"
                        />
                    </div>
                    <div class="form-inline top-buffer" id="logintext">
                        <label class="checkbox loginlabel">
                            <input type="checkbox" name="remember" ref="remember" checked value="1" /> 记住密码
                        </label>
                    </div>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
let Base64 = require('js-base64').Base64;
export default {
    name: 'Home',
    props: ['Home'],
    data() {
        return {
            isLogin: false,
        };
    },
    created() {
        this.$http.post('http://111.204.156.11:8192/checklogin',
                    {
                        name: 'zhangdi',
                        pw: Base64.encode('xy2062Z&Z'),
                        crypted: true,
                    },
                    { emulateJSON: true },
                )
                .then((data) => {
                    console.log(data);
                    let dataArr = data.data.split('&&');
                    let isOK = dataArr[0];
                    let pwd = dataArr[1];
                    //验证成功
                    if (isOK == 'success') {
                        //记住密码选中,保存七天
                        if (false) {
                            this.set('username', username, 7);
                            this.set('password', pwd, 7);
                        }
                        //关闭登陆界面
                        this.loginClose();
                        //立即体验点击事件
                        this.$emit('gohome', {param: false});
                    } else {
                        localStorage.clear();
                        alert('账号与密码不匹配!');
                    }
                })
                .catch(function(response) {
                    console.log(response);
                });
    },
    methods: {
        //点击立即体验时，判断是否已登录
        checkLogin() {
            let getUsername = this.get('username');
            if (getUsername) {
                let username = getUsername;
                let password = this.get('password');
                this.checkUser(username, password);
            } else {
                this.isLogin = true;
                this.$emit('home', { param: true });
            }
        },
        //关闭登陆界面
        loginClose() {
            // this.$refs.username.value = '';
            // this.$refs.password.value = '';
            this.isLogin = false;
            this.$emit('home', { param: false });
        },
        //提交验证
        checkSubmit() {
            //获取用户输入的账号密码
            let username = this.$refs.username.value;
            let password = this.$refs.password.value;
            let remember = this.$refs.remember.checked;

            if (username && password) {
                //对密码进行加密
                let pwd = Base64.encode(password);
                this.checkUser(username, pwd, remember, true);
            } else {
                alert('用户名和密码不能为空！');
                return false;
            }
            return false;
        },

        /**
         *@description 验证用户名与密码是否匹配
         * @param {string} username
         * @param {string} password
         */
        checkUser(username, password, remember, iscrypted) {
            if (!iscrypted) {
                iscrypted = '';
            }
            this.$http.post('http://111.204.156.11:8192/checklogin',
                    {
                        name: username,
                        pw: password,
                        crypted: iscrypted,
                    },
                    { emulateJSON: true },
                )
                .then((data) => {
                    console.log(data);
                    let dataArr = data.data.split('&&');
                    let isOK = dataArr[0];
                    let pwd = dataArr[1];
                    //验证成功
                    if (isOK == 'success') {
                        //记住密码选中,保存七天
                        if (remember) {
                            this.set('username', username, 7);
                            this.set('password', pwd, 7);
                        }
                        //关闭登陆界面
                        this.loginClose();
                        //立即体验点击事件
                        this.$emit('gohome', {param: false});
                    } else {
                        localStorage.clear();
                        alert('账号与密码不匹配!');
                    }
                })
                .catch(function(response) {
                    console.log(response);
                });
        },
        //封装过期控制代码
        //存储信息到localStorage
        set(key, value, day) {
            //默认存储1天
            if (!day) {
                day = 1;
            }
            var expires = day * 24 * 60 * 60 * 1000;
            //var expires = 10 * 1000;
            var curTime = new Date().getTime() + expires;
            localStorage.setItem(
                key,
                JSON.stringify({
                    data: value,
                    time: curTime,
                }),
            );
        },
        //从localStorage读信息，过期则删除
        get(key) {
            var data = localStorage.getItem(key);
            if (data) {
                var dataObj = JSON.parse(data);
                if (new Date().getTime() >= dataObj.time) {
                    localStorage.removeItem(key);
                } else {
                    var dataObjDatatoJson = dataObj.data;
                    return dataObjDatatoJson;
                }
            }
        },

        //退出登陆
        loginOut() {
            localStorage.clear();
            // goHome()
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
