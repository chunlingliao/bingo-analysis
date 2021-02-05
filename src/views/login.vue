<template>
    <div>
        <div class="main">
            <div class="login-wrap">
                <div class="login-logo mb-3 text-center"><img src="images/login-logo.png" alt=""></div>
                <div class="input-region">
                  <input class="form-control form-control-sm" type="text" placeholder="請輸入序號" v-model="serialNumber">
                  <button class="btn btn-primary w-100 mt-3" type="button" disabled v-if="loadingStatus">
                    <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
                    <span class="sr-only">Loading...</span>
                  </button>
                  <button class="btn btn-login w-100 mt-3" type="button" @click="login" v-else>登入</button>
                </div>
            </div>
            <div class="ball01 animate__animated animate__zoomIn "><img src="images/ball01.png" alt=""></div>
            <div class="ball02 animate__animated animate__zoomIn"><img src="images/ball02.png" alt=""></div>
            <div class="ball03 animate__animated animate__zoomIn"><img src="images/ball03.png" alt=""></div>
            <div class="ball04 animate__animated animate__zoomIn"><img src="images/ball04.png" alt=""></div>
            <div class="ball05 animate__animated animate__zoomIn"><img src="images/ball05.png" alt=""></div>
            <div class="ball06 animate__animated animate__zoomIn"><img src="images/ball06.png" alt=""></div>
            <div class="ball07 animate__animated animate__zoomIn"><img src="images/ball07.png" alt=""></div>
            <div class="ball08 animate__animated animate__zoomIn"><img src="images/ball08.png" alt=""></div>
            <div class="ball09 animate__animated animate__zoomIn"><img src="images/ball09.png" alt=""></div>
        </div>
    </div>
</template>
<script>
import animated from 'animate.css'
// import axios from 'axios'

// const $axios = axios.create({
//   baseURL: process.env.VUE_APP_API_URL
// })

export default {
  name: 'login',
  data: function () {
    return {
      /* 測試序號 */
      // qwert16888

      // 輸入序號
      serialNumber: '',
      // 載入狀態
      loadingStatus: '',
      // 錯誤訊息
      errorMsg: {
        login: {
          title: '登入錯誤',
          contents: ''
        },
        otherError: {
          contents: '無法得知的錯誤，請聯絡客服'
        }
      }
    }
  },
  mounted () {
    // 清除資訊
    localStorage.clear()
  },
  methods: {
    //登入邏輯 假資料
      login(){
        // 尚未輸入序號
        if (!this.serialNumber) {
          this.$toastr.error('尚未輸入帳號')
          return
        }
        if (this.serialNumber ==='' && this.serialNumber !=='qwert16888' ) {
          // 錯誤訊息
          console.log(this.serialNumber)
          this.$toastr.error(`${this.serialNumber} 登入失敗！請重新登入`)
        } else if (this.serialNumber ==='qwert16888') { 
          // success
          this.$toastr.success(`${this.serialNumber} 登入成功`)
          localStorage.setItem('login','true')
          // 登入成功跳轉內頁
          this.$router.push({
            path: '/index'
          })
        }
      },
    // login () {
    //   if (!this.serialNumber) {
    //     this.$toastr.warning('請輸入序號')
    //     return
    //   }
    //   // 載入狀態(開始)
    //   this.loadingStatus = true
    //   const headers = { 'Content-Type': 'multipart/form-data' }
    //   let bodyFormData = new FormData()
    //   bodyFormData.append('token', this.serialNumber)
    //   $axios.post('/check_token', bodyFormData, { headers: headers })
    //     .then(res => {
    //       // console.log('login res:', res.data.success)
    //       if (!res.data.hasOwnProperty('success')) {
    //         // 載入狀態(結束)
    //         this.loadingStatus = false
    //         return
    //       }
    //       let loginType = ''
    //       // 普通使用者驗證
    //       if (res.data.success.hasOwnProperty('lost_days') && Number(res.data.success.lost_days) > 0) {
    //         loginType = 'general-user'
    //       // 超級使用者驗證
    //       } else if (res.data.success.hasOwnProperty('super_user') && res.data.success.super_user) {
    //         loginType = 'super-user'
    //         localStorage.setItem('su_token', res.data.success.tokens)
    //       }
    //       if (loginType) {
    //         // 登入成功儲存使用者資訊
    //         localStorage.setItem('bingo.login.type', loginType)
    //         // 登入成功跳轉內頁
    //         this.$router.push({
    //           path: '/'
    //         })
    //         // 載入狀態(結束)
    //         this.loadingStatus = false
    //       }
    //     })
    //     .catch(err => {
    //       // 載入狀態(結束)
    //       this.loadingStatus = false
    //       if (err.hasOwnProperty('response')) {
    //         console.log('err response:', err.response)
    //         if (!err.response) {
    //           this.$toastr.error(`${this.errorMsg.login.title}：${this.errorMsg.otherError.contents}`)
    //           return
    //         }
    //         if (!err.response.data.hasOwnProperty('false')) return
    //         if (err.response.data.false.hasOwnProperty('msg')) {
    //           this.clearInput()
    //           this.$toastr.error(`${this.errorMsg.login.title}：${err.response.data.false.msg}`)
    //         }
    //       } else {
    //         console.log('err:', err)
    //       }
    //     })
    // },
    clearInput () {
      this.serialNumber = ''
    }
  }
}
</script>
