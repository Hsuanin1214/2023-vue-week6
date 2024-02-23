<template>
    <h1>這是後台 商品</h1>
</template>

<script>
import axios from 'axios'
const { VITE_URL } = import.meta.env
export default {
  data () {
    return {
      url: VITE_URL
    }
  },
  methods: {
    checkLogin (params) {
      console.log(this.url)
      axios
        .post(`${this.url}/api/user/check`)
        // 成功的結果
        .then((res) => {
          console.log(res)
          // this.getProduct()
        })
        // 失敗結果
        .catch((error) => {
          console.dir(error) // 用dir可以展開資訊
          alert('未登入')
          this.$router.push('/login')
        })
    }
  },
  mounted () {
    const token = document.cookie.replace(
      /(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/, '$1')
    // console.log(token);
    axios.defaults.headers.common.Authorization = token
    this.checkLogin()
  }
}
</script>
