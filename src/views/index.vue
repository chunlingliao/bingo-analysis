<template>
<div>
  <div class="text-left header">
    <div class="container">
    <div class="row">
        <div class="col-6 bingo-title">
          <b>BINGO</b>
        </div>
        <div class="col-6">
          <div class="float-right">
            <router-link to="/admin" class="badge badge-light p-2 mr-2" v-if="checkSuperUser">進入後台</router-link>
            <router-link to="/login" class="badge badge-light p-2" @click="logout">登出</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="container">
    <!-- 第一塊 -->
    <div class="row bingo-wrap no-gutters mt-3 mb-3">
      <div class="col-sm-3">
        <div class="mb-3 font-weight-bold">距離下次開獎剩餘時間</div>
        <div class="d-flex justify-content-center">
          <div class="time float-left">11</div>
          <div class="time-sign float-left mr-1 ml-1">:</div>
          <div class="time float-left">11</div>
        </div>
      </div>
      
      <div class="col-sm-5">
        <div class="font-weight-bold mb-3 mt-3 mt-sm-0">第{{ history[0].draw_number }}期</div>
          <ul class="nav number-periods-lottery">
            <li v-for="balls in history[0].balls" :key="balls" 
            :class="['l-bingo-number number-inplay',{'super-number-inplay': Number(history[0].super_ball) === Number(balls)}]">{{ balls }}</li>
            <!-- <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number super-number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li>
            <li class="l-bingo-number number-inplay">11</li> -->
          </ul>
      </div>

      <div class="col-sm-2 col-6 mt-3 mt-sm-0">
        <div class="font-weight-bold mb-2">超級獎號</div>
        <div class="large-super-number">{{ history[0].super_ball }}</div>
      </div>
      <div class="col-sm-2 col-6 mt-3 mt-sm-0">
        <div class="font-weight-bold mb-3">獎號總和</div>
        <div class="text-primary number-total font-weight-bold">{{ history[0].total_number }}</div>
      </div>
    </div>

    <!-- 第二塊預期總和 -->
    <div class="expected-sum mb-3">
      <div class="text-left float-left expected-sum-text font-weight-bold">
        {{ estimate.draw_number }}期預測總和 {{ estimate.even }} {{ estimate.size }}
        <!-- <span v-if="estimate.total_number <= '810'">
          小
        </span>
        <span v-else>
          大
        </span> -->
      </div>
        <ul class="nav">
          <li v-for="balls in estimate.balls" :key="balls" 
            :class="['l-bingo-number',{'super-number': Number(estimate.super_ball) === Number(balls)}]">{{ balls }}</li>
        </ul>
    </div>

    <!-- 第三區塊導覽列 -->
    <div>
      <ul class="nav nav-pills mb-3" id="pills-tab" role="tablist">
        <li class="nav-item">
          <a class="nav-link active" id="pills-history-tab" data-toggle="pill" href="#pills-history" role="tab" aria-controls="pills-history" aria-selected="true">歷史開獎紀錄</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" id="pills-super-tab" data-toggle="pill" href="#pills-super" role="tab" aria-controls="pills-super" aria-selected="false">超級獎號走勢</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" id="pills-hot-tab" data-toggle="pill" href="#pills-hot" role="tab" aria-controls="pills-hot" aria-selected="false">冷熱碼</a>
        </li>
      </ul>
      <div class="tab-content" id="pills-tabContent">
        <!-- 歷史開獎紀錄 -->
        <div class="tab-pane fade show active" id="pills-history" role="tabpanel" aria-labelledby="pills-history-tab">
          <div class="table-responsive">
            <table class="table table-striped">
              <thead>
                <tr>
                  <th scope="col">類別</th>
                  <th scope="col">開獎號碼</th>
                  <th scope="col">超級號碼</th>
                  <th scope="col">獎號總和</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, i) in history" :key="i">
                  <td class="font-weight-bold period">
                    第{{ item.draw_number }}期</td>
                  <td>
                    <ul class="nav d-flex justify-content-center win-number history-lottery">
                      <li v-for="balls in item.balls" :key="balls"
                        :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(balls)}]">{{ balls }}</li>
                      <!-- <li class="l-bingo-number super-number">11</li> -->
                    </ul>
                  </td>
                  <td>
                    <div class="history-super-number">{{ item.super_ball }}</div>
                  </td>
                  <td><div class="history-number-total">{{ item.total_number }}</div></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- 超級開獎號碼 -->
        <div class="tab-pane fade" id="pills-super" role="tabpanel" aria-labelledby="pills-super-tab">
          <div class="super-tab-bg">
            <div class="mb-5">
              <canvas id="myChart"></canvas>
            </div>
          </div>
        </div>
        <!-- 冷熱碼 -->
        <div class="tab-pane fade" id="pills-hot" role="tabpanel" aria-labelledby="pills-hot-tab">
          <div class="table-responsive">
            <table class="table table-striped">
              <tbody>
                <tr v-for="(item , i) in hotNumber" :key="i">
                  <td v-for="(number, j) in item" :key="j">
                    <div class="hotCold-number">
                      <div class="l-bingo-number float-left">{{ number.ball }}</div>
                      <div class="ball-type">{{ number.type }}次</div>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
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
import Chart from 'chart.js'

export default {
  name: "",
  props: {},
  data: function() {
    // 資料
    return {
      // 預測號碼
      estimate:
        {       
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069700",
          "super_ball": "7",
          "even":"單",
          "size":'大',
          "total_number": "811"
        },
      // 歷史號碼
      history:[
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069751",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "1",
          "total_number": "817"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069752",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "3",
          "total_number": "347"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069753",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "78",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 8, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069754",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "8",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 66, 68, 69, 71, 78],
          "draw_number": "109069755",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "66",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 9, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069756",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "9",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069757",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "45",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 62, 68, 69, 71, 78],
          "draw_number": "109069758",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "62",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 44, 47, 48, 63, 68, 69, 71, 78],
          "draw_number": "109069759",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "44",
          "total_number": "555"
        },
        {
          "balls": [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 58, 63, 68, 69, 71, 78],
          "draw_number": "109069760",
          "game_time": "Wed, 09 Dec 2020 17:10:00 GMT",
          "super_ball": "58",
          "total_number": "555"
        }
      ],
      hotNumber2:
      {
        "1": 5,
        "2": 9,
        "3": 10,
        "4": 10,
        "5": 5,
        "6": 9,
        "7": 10,
        "8": 10
      },
      hotNumber:[
        [{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'02', type:'20'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'03', type:'30'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'04', type:'40'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'05', type:'50'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'06', type:'60'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'07', type:'20'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}],
        [{ ball:'08', type:'20'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},
        { ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'},{ ball:'01', type:'10'}]
      ],
      chartLabels: [],
      chartSuperBalls: [],
      checkSuperUser: false
    };
  },
  components: {
    // f2ecommonMask //1.個別引入
  },
  watch: {
    //監聽值
  },
  computed: {
    //相依的資料改變時才做計算方法
  },
  methods: {
    // 初始
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
    console.log(window.customElements)
    if(!localStorage.getItem('login')) 
      this.$router.push({
        path: '/login'
      })

    this.checkSuperUser = localStorage.getItem('login')

    // for (let i = 0; i <= 39; i++) {
    var Len = this.history.length <= 40 ? this.history.length : 40
    console.log('Len:', Len)
    for (let i = 0; i < Len; i++) {
      // console.log(i)
      console.log('draw_number:', i, this.history[i].draw_number, this.history[i].draw_number.slice(-2))
      this.chartLabels.push(this.history[i].draw_number.slice(-2))
      this.chartSuperBalls.push(this.history[i].super_ball)
    }
    
    var ctx2 = document.getElementById("myChart");

    var myChart = new Chart(ctx2, {
        type: "line",
        data: {
            // labels: ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", "11", "12", "13", "14", "15", "16", "17", "18", "19", "20"],
            labels: this.chartLabels,
            datasets: [
                {
                  label: "超級獎號:",
                  // backgroundColor: "rgba(225,10,10,0.3)",
                  borderColor: "#057eff",
                  // borderWidth: 1,
                  // pointStrokeColor: "#fff",
                  // pointStyle: "crossRot",
                  // data: [65, 59, 0, 51, 56, 10, 40, 22, 32, 54, 10, 30],
                  data: this.chartSuperBalls,
                  cubicInterpolationMode: "monotone",
                  spanGaps: "false",
                  fill: "false"
                }
            ]
        },
        options: {
          legend: {
            display: false
          },
        scales: {
            yAxes: [{
                ticks: {
                    suggestedMin: 0,
                    suggestedMax: 80
                }
            }]
          }
      }
    });

    // for(item in history){

    // }


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

<style>
</style>