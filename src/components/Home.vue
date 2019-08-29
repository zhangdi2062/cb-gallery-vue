<template>
  <div>
    <Logo ref="logo" @home=home></Logo>
    <Header @home=login ref="header"></Header>
    <Content ref="content" ></Content>
    <Login @home=header @gohome=home ref="login"></Login>
    <Footer ref="footer"></Footer>
  </div>
  
</template>

<script>
import Logo from './Logo'
import Header from './Header.vue'
import Content from './Content'
import Footer from './Footer'
import Login from './Login'

export default {
  name: 'Home',
  props: {
    msg: String
  },
  components: {
    Header,
    Logo,
    Content,
    Login,
    Footer,
  },
  methods: {
    login() {
      this.$refs.login.checkLogin()
    },
    header({param}) {
      // if (param) {
        this.$refs.header.isLogin = param
        this.$refs.logo.isLogin = !param
      // }
    },
    home({param}) {
      this.$refs.content.isShow = !param
      this.$refs.footer.isShow = !param
      this.$refs.header.isShow = param
      this.$refs.logo.isShow = param
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ul {
  list-style-type: none;
  padding: 0;
}
</style>
