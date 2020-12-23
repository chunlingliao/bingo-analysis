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
        <div class="font-weight-bold mb-3 mt-3 mt-sm-0">第{{ draw_number }}期</div>
          <ul class="nav number-periods-lottery">
            <li class="l-bingo-number number-inplay" v-for="i in balls" :key="i">{{ i }}</li>
            <!-- <li class="l-bingo-number super-number-inplay">11</li> -->
          </ul>
      </div>

      <div class="col-sm-2 col-6 mt-3 mt-sm-0">
        <div class="font-weight-bold mb-2">超級獎號</div>
        <div class="large-super-number">{{ super_ball }}</div>
      </div>
      <div class="col-sm-2 col-6 mt-3 mt-sm-0">
        <div class="font-weight-bold mb-3">獎號總和</div>
        <div class="text-primary number-total font-weight-bold">{{ total_number }}</div>
      </div>
    </div>

    <!-- 第二塊預期總和 -->
    <div class="expected-sum mb-3">
      <div class="text-left float-left expected-sum-text font-weight-bold">{{ draw_number }}期預測總和 小</div>
        <ul class="nav">
          <li class="l-bingo-number" v-for="i in balls" :key="i">{{ i }}</li>
          <!-- <li class="l-bingo-number super-number">11</li> -->
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
                <tr v-for="(item, i) in historyTable" :key="i">
                  <td class="font-weight-bold period">第{{ item.draw_number }}期</td>
                  <td>
                    <ul class="nav d-flex justify-content-center win-number history-lottery">
                      <li class="l-bingo-number"  
                      v-for="balls in item.balls" :key="balls">{{ balls }}</li>
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
      // ## history/post & get
      balls: [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
      draw_number: "109069751",
      game_time: "Wed, 09 Dec 2020 17:10:00 GMT",
      super_ball: "20",
      total_number: "747",
      // ## predict/get
      balls: [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
      draw_number: "109069751",
      total_number: "747",

      historyTable:[{
        balls: [1, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
        draw_number: "109069751",
        game_time: "Wed, 09 Dec 2020 17:10:00 GMT",
        super_ball: "20",
        total_number: "747",
      },
      {
        balls: [2, 3, 7, 12, 17, 19, 20, 31, 33, 34, 38, 43, 45, 47, 48, 63, 68, 69, 71, 78],
        draw_number: "109069752",
        game_time: "Wed, 09 Dec 2020 17:10:00 GMT",
        super_ball: "30",
        total_number: "800",
      },
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
            labels: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
            datasets: [
                {
                  // label: "超級獎號",
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

      // var newStr = JSON.stringify(historyTable)
      // console.log(newStr)

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