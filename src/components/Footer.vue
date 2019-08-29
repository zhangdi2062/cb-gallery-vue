<template>
   <footer v-if="isShow" class="container footer-box" id="footer">
        <div class="row">
            <div class="col-sm-4 footer1">
                <div>
                    <span class="uin-word1" @click="goUinnova">优锘科技</span>
                    <span class="uin-word2">帮助人们更好的认识和管理数据化新世界</span>
                </div>
            </div>
            <div class="col-sm-2 footer2">
                <img src="/static/img/tel.png" width="24px" height="24px">&nbsp;400-051-0152
            </div>
            <div class="col-sm-2 footer3">
                <img src="/static/img/email.png" width="24px" height="24px">&nbsp;info@uinnova.com
            </div>
            <div class="col-sm-4 footer4">
                <img src="/static/img/map.png" width="24px" height="24px">&nbsp;北京市朝阳区花家地北里14号北京国际画材中心五层
            </div>
        </div>
    </footer>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  },
  data() {
      return {
          isShow: false
      }
  },
  methods: {
      goUinnova() {
          window.open("http://www.uinnova.cn/")
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
