<template>
<div>
  <div class="text-left header">
    <div class="container">
      <div class="row">
        <div class="col-6 bingo-title">
          賓果後台管理系統
        </div>
        <div class="col-6">
          <div class="float-right">
            <router-link to="/" class="badge badge-light p-2 mr-2" >進入前台</router-link>
            <router-link to="/login" class="badge badge-light p-2" @click="logout">登出</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="container">
    <div class="form-group mt-4">
      <label for="lname" class="d-inline-block">新增</label>
      <input type="text" v-model="num" class="form-control mx-sm-3 d-inline-block" placeholder="筆數">
      <label for="lname" class="d-inline-block">筆序號</label>
      <button type="submit" class="btn btn-primary mb-2 d-inline-block ml-2 mr-5" @click="insert()">新增</button>

      <select v-model="selected" class="form-control filterSelect d-inline-block">
          <option v-for="(option, i) in options" v-bind:value="option.value" :key="i">
            {{ option.text }}
          </option>
      </select>
      <button type="button" class="btn btn-info float-right" @click="download()">下載</button>
    </div>
      <div class="text-muted text-left mb-4 tip">
        *必須為數字
      </div>
  </div>

  <!-- 表格 -->
  <div class="tab-pane fade show active container" id="pills-history" role="tabpanel" aria-labelledby="pills-history-tab">
    <div class="table-responsive">
      <table class="table table-striped text-center">
        <thead>
          <tr>
            <th scope="col">開始日期</th>
            <th scope="col">預計過期日</th>
            <th scope="col">序號</th>
            <th scope="col">是否啟用</th>
            <th scope="col">刪除</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, i) in this.search" :key="i">
            <td class="">
              {{ item.created_at }}
            </td>
            <td>
              {{ item.end_at }}
            </td>
            <td>
              {{ item.token }}
            </td>
            <td>
              <div v-if="item.used">
                <i class="fas fa-check-circle"></i>
              </div>
              <div v-else>
                <i class="fas fa-times-circle"></i>
              </div>
            </td>
            <!-- <td>
              <div @click="deleteList()"><i class="fas fa-trash"></i></div>
            </td> -->

            <td>
              <!-- Button trigger modal -->
              <div data-toggle="modal" data-target="#deleteModal" @click="getToken(i)"><i class="fas fa-trash"></i></div>
            </td>
          </tr>
        </tbody>
      </table>

      <!-- Modal -->
      <div class="modal fade" id="deleteModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">序號刪除</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              您確定要刪除序號嗎？
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">取消</button>
              <button type="button" class="btn btn-primary" @click="deleteList()">確定刪除</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <a href="#" class="toTop" title="GoTop" style="display: inline;"><span></span></a>
</div>

</template>

<script>
import $ from 'jquery'
// import axios from "axios";
// import toastr from 'toastr'
// const instance = axios.create({
//   withCredentials: false
// })

export default {
  name: "",
  props: {},
  data: function() {
    // 資料
    return {
      src: "" ,//追蹤 store用
      selected: 'all',
        options: [
        { text: '全部', value: 'all' },
        { text: '使用中', value: 'used' },
        { text: '未使用', value: 'not_used' }
      ],

      search:[
        { created_at:'2021-01-01', end_at:'2021-02-02', token:'123', used: true },
        { created_at:'2021-01-01', end_at:'2021-02-02', token:'456', used: true },
        { created_at:'2021-01-01', end_at:'2021-02-02', token:'789', used: true },
        { created_at:'2021-01-01', end_at:'2021-02-02', token:'9999', used: false },
        { created_at:'2021-01-01', end_at:'2021-02-02', token:'asdf', used: false }
      ],
      searchOri: [],
      num:'',
      // token:'',
      deleteToken: '',
      // su_token: localStorage.getItem('su_token')
    };
  },
  components: {
    // f2ecommonMask //1.個別引入
  },
  watch: {
    //監聽值
    // 切換列表選擇
    'selected' (value) {
      let items = []
      if (value === 'used') {
        for (let item in this.searchOri) {
          if (this.searchOri[item].used) items.push(this.searchOri[item])
        }
      } else if (value === 'not_used') {
        for (let item in this.searchOri) {
          if (!this.searchOri[item].used) items.push(this.searchOri[item])
        }
      } else if (value === 'all') {
        for (let item in this.searchOri) {
          items.push(this.searchOri[item])
        }
      }
      this.search = items
    }
  },
  computed: {
    //相依的資料改變時才做計算方法
  },
  methods: {
    // 初始
    // getSearchList () {
    //   // console.log(this.selected)
    //   axios.get(process.env.VUE_APP_API_URL + "/search_data"+"?query_type="+this.selected+"&su_token="+this.su_token).then(res => {
    //     this.search = res.data.success
    //     // console.log('search res:', res.data.success)
    //   });
    // },

    // insert () {
    //   const headers = { 'Content-Type': 'multipart/form-data' }
    //   let insertFormData = new FormData()
    //   insertFormData.append('nums', this.num)
    //   insertFormData.append('su_token', this.su_token)
    //   axios.post(process.env.VUE_APP_API_URL + "/insert", insertFormData, { headers: headers })
    //   .then(res => {
    //     // console.log('insert:',res.data.success)
    //     // alert('新增成功')
    //     this.$toastr.success( "新增成功" )
    //     this.getSearchList()
    //   });
    // },

    // deleteList () {
    //   // console.log(this.deleteToken)
    //     axios.delete(process.env.VUE_APP_API_URL + "/delete"+"?token="+ this.deleteToken+"&su_token="+this.su_token).then(res => {
    //     // console.log('delete:',res.data.success)
    //     $('#deleteModal').modal('hide')
    //     this.$toastr.success('刪除成功')
    //     this.getSearchList()
    //   });
    // },

    // 上正式的話要改連結
    // download () {
    //   axios.get(process.env.VUE_APP_API_URL + "/download"+"?su_token="+this.su_token).then(res => {
    //     // console.log('download:',res.config.url)
    //     // 正式時啟用
    //     window.location = res.config.url

    //     // 測試用連結
    //     // window.location = 'http://abc.bingowin.org/download'
    //   });
    // },

    // download (){
    //   axios({
    //       url:process.env.VUE_APP_API_URL+'/download',
    //       method:'GET',
    //       // responseType: 'blob'
    //   })
    //   .then((response) => {
    //       console.log('download:',response)
    //     })
    // }

    // 刪除選取 token
    // getToken (value) {
    //   // console.log('>>',value)
    //   this.deleteToken = value
    // },

    getToken (value) {
      console.log('>>',value)
      this.deleteToken = value
    },

    // logout () {
    //   // 登出清除使用者資訊
    //   axios.get(process.env.VUE_APP_API_URL + "/su_logout").then(res => {
    //     // console.log('loginout:',res.success)
    //     localStorage.clear()
    //   });
    // }
    insert() {
      for(let i = 0; i <  this.num; i++){
        this.search.push({ created_at:'2021-01-01', end_at:'2021-02-02', token:`123-${i}`, used: false })
      }
      this.searchOri = this.search
    },

    deleteList () {
      console.log('this.deleteToken:',this.deleteToken)
        this.search.splice(this.deleteToken, 1)
        $('#deleteModal').modal('hide')
        this.$toastr.success('刪除成功')
    },
    logout () {
      // 登出清除使用者資訊
        localStorage.clear()
    }
  },
  //BEGIN--生命週期
  beforeCreate: function() {
    //實體初始化
  },
  created: function() {
    //實體建立完成。資料 $data 已可取得，但 $el 屬性還未被建立。
    this.src = this.$options.__file ;
  },
  beforeMount: function() {
    //執行元素掛載之前。
  },
  mounted: function() {
    //元素已掛載， $el 被建立。
    // console.log(window.customElements)
    // this.getSearchList()
    this.searchOri = this.search

    //gotop
    $(window).scroll(function () {
      if ($(this).scrollTop() > 100) {
        $('.toTop').fadeIn()
      } else {
        $('.toTop').fadeOut()
      }
    })
    $('.toTop').click(function () {
      $('html, body').animate({
        scrollTop: 0
      }, 800)
      return false
    })

    // const headers = { 'Content-Type': 'multipart/form-data' }
    //   let bodyFormData = new FormData()
    //   bodyFormData.append('token', '702438b1-c3ec-4c73-b7e5-761f106d6def')
    //   axios.post(process.env.VUE_APP_API_URL + '/check_token', bodyFormData, { headers: headers })
    //     .then(res => {
    //       console.log('login res:', res.data.success)
    //       this.getSearchList()
    //     })
    //     .catch(err => {
    //       // console.log('err:', err)
    //       if (err.hasOwnProperty('response')) {
    //         // console.log('err response:', err.response)
    //         if (!err.response.data.hasOwnProperty('false')) return
    //         if (err.response.data.false.hasOwnProperty('msg')) {
    //           alert(err.response.data.false.msg)
    //         }
    //       }
    //     })


    // 下載功能
    // let downloadBtn = document.querySelector(".downloadBtn");
    // downloadBtn.addEventListener("click", downloadFile);
    // function downloadFile() {
    //   //藉型別陣列建構的 blob 來建立 URL
    //   let fileName = "fileName.csv";
    //   const data = getRandomData();
    //   let blob = new Blob([data], {
    //     type: "application/octet-stream"
    //   });
    //   var href = URL.createObjectURL(blob);
    //   // 從 Blob 取出資料
    //   var link = document.createElement("a");
    //   document.body.appendChild(link);
    //   link.href = href;
    //   link.download = fileName;
    //   link.click();
    //   console.log('blob:',blob)
    //   console.log('href:',href)
    // }



    // function download(){
    //   axios({
    //       url:'https://source.unsplash.com/random/500x500',
    //       method:'GET',
    //       responseType: 'blob'
    //   })
    //   .then((response) => {
    //         const url = window.URL
    //         .createObjectURL(new Blob([response.data]));
    //           const link = document.createElement('a');
    //           link.href = url;
    //           link.setAttribute('download', 'image.jpg');
    //           document.body.appendChild(link);
    //           link.click();
    //     })
    //   }

    //假資料
    // function getRandomData() {
    // var header = "RandomHeader";
    // var data = "";
    //   for (let i = 0; i < 5; i++) {
    //     for (var j = 0; j < 2; j++) {
    //       if (j > 0) {
    //         data = data + ",";
    //       }
    //       data = data + "Item" + i + "_" + j;
    //     }
    //   }
    //   return header + data;
    // }
  },
  beforeUpdate: function() {
    //當資料變化時被呼叫，還不會描繪 View。
  },
  updated: function() {
    //當資料變化時被呼叫，還不會描繪 View。
  },
  beforeDestroy: function() {
    //實體還可使用。
  },
  destroyed: function() {
    //實體銷毀。
  }
  //END--生命週期
};
</script>

<style lang="scss" scoped>
</style>
