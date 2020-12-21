<template>
<div>
  <div class="text-left header">
    <div class="container">賓果賓果輔助系統</div>
  </div>
  <div class="container">
    <div class="text-left text-primary mt-3 mb-3">賓果賓果</div>
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
            <li v-for="balls in history[0].balls" :key="balls" class="l-bingo-number number-inplay">{{ balls }}</li>
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
                <tr v-for="item in history" :key="item">
                  <td class="font-weight-bold period">
                    第{{ item.draw_number }}期</td>
                  <td>
                    <ul class="nav d-flex justify-content-center win-number history-lottery">
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[0])}]">{{ item.balls[0] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[1])}]">{{ item.balls[1] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[2])}]">{{ item.balls[2] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[3])}]">{{ item.balls[3] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[4])}]">{{ item.balls[4] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[5])}]">{{ item.balls[5] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[6])}]">{{ item.balls[6] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[7])}]">{{ item.balls[7] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[8])}]">{{ item.balls[8] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[9])}]">{{ item.balls[9] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[10])}]">{{ item.balls[10] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[11])}]">{{ item.balls[11] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[12])}]">{{ item.balls[12] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[13])}]">{{ item.balls[13] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[14])}]">{{ item.balls[14] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[15])}]">{{ item.balls[15] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[16])}]">{{ item.balls[16] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[17])}]">{{ item.balls[17] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[18])}]">{{ item.balls[18] }}</li>
                      <li :class="['l-bingo-number',{'super-number': Number(item.super_ball) === Number(item.balls[19])}]">{{ item.balls[19] }}</li>
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
        }
      ],
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
      ]
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
    
    var ctx2 = document.getElementById("myChart");

    var myChart = new Chart(ctx2, {
        type: "line",
        data: {
            labels: ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", "11", "12", "13", "14", "15", "16", "17", "18", "19", "20"],
            datasets: [
                {
                  label: "超級獎號:",
                  // backgroundColor: "rgba(225,10,10,0.3)",
                  borderColor: "#057eff",
                  // borderWidth: 1,
                  // pointStrokeColor: "#fff",
                  // pointStyle: "crossRot",
                  data: [65, 59, 0, 51, 56, 10, 40, 22, 32, 54, 10, 30],
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