<template>
  <div class="tinyBingo">
    <header>
      <nav class="navbar navbar-primary bg-primary text-white">
        <div class="container">
          賓果賓果輔助系統
        </div>
      </nav>
    </header>

    <main>
      <div class="container">
        <p class="mt-3 text-left text-primary">賓果賓果</p>

        <!-- 當前資訊區 -->
        <div class="currentInfo mt-3">
          <div class="row">
            <!-- 倒數器 -->
            <div class="countdown col-md-3 col-sm-12 pb-3">
              <p>距離下期開獎剩餘</p>
              <div class="d-flex justify-content-center pt-2 pb-2">
                <span class="time font-weight-bold">
                  03
                </span>
                <span class="timeColon">:</span>
                <span class="time font-weight-bold">
                  56
                </span>
              </div>
            </div>

            <!-- 當前期號 -->
            <div class="currentNumber col-md-5 col-sm-12 pb-3 text-center">
              <p>第<span>000000005</span>期</p>
              <div class="d-flex justify-content-center pt-2 pb-2">
                <div class="ball w-320">
                  <div class="defaultBall">01</div>
                  <div class="defaultBall">02</div>
                  <div class="defaultBall">03</div>
                  <div class="defaultBall">04</div>
                  <div class="defaultBall">05</div>
                  <div class="defaultBall">06</div>
                  <div class="defaultBall">07</div>
                  <div class="defaultBall">08</div>
                  <div class="defaultBall">09</div>
                  <div class="defaultBall">10</div>
                  <div class="defaultBall">11</div>
                  <div class="defaultBall">12</div>
                  <div class="defaultBall">13</div>
                  <div class="defaultBall">14</div>
                  <div class="defaultBall">15</div>
                  <div class="defaultBall">16</div>
                  <div class="defaultBall">17</div>
                  <div class="defaultBall">18</div>
                  <div class="defaultBall">19</div>
                  <div class="defaultBall specialBall">20</div>
                </div>
              </div>
            </div>

            <!-- 超級獎號 -->
            <div class="col-md-2 col-6 pb-3">
              <p>超級獎號</p>
              <div class="d-flex justify-content-center">
                <div class="superBall font-weight-bold">
                  20
                </div>
              </div>
            </div>

            <!-- 獎號總和 -->
            <div class="col-md-2 col-6">
              <p>獎號總和</p>
              <div class="d-flex justify-content-center">
                <div class="totalBall font-weight-bold text-primary">
                  210
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- 預測資訊區 -->
        <div class="predictionInfo mt-3">
          <div class="text-left d-flex align-items-center">
            <div class="predictionNumber ml-4">000000006期預測總和 小</div>
            <div class="ball ml-4">
              <div class="defaultBall blackTextBall">01</div>
              <div class="defaultBall blackTextBall">02</div>
              <div class="defaultBall blackTextBall">03</div>
              <div class="defaultBall blackTextBall">04</div>
              <div class="defaultBall blackTextBall">05</div>
              <div class="defaultBall blackTextBall">06</div>
              <div class="defaultBall blackTextBall">07</div>
              <div class="defaultBall blackTextBall specialBall">08</div>
              <div class="defaultBall blackTextBall">09</div>
              <div class="defaultBall blackTextBall">10</div>
              <div class="defaultBall blackTextBall">11</div>
              <div class="defaultBall blackTextBall">12</div>
              <div class="defaultBall blackTextBall">13</div>
              <div class="defaultBall blackTextBall">14</div>
              <div class="defaultBall blackTextBall">15</div>
              <div class="defaultBall blackTextBall">16</div>
              <div class="defaultBall blackTextBall">17</div>
              <div class="defaultBall blackTextBall">18</div>
              <div class="defaultBall blackTextBall">19</div>
              <div class="defaultBall blackTextBall">20</div>
            </div>
          </div>
        </div>

        <!-- 分頁分析區 -->
        <ul class="nav nav-pills mt-3 mb-3" id="pills-tab" role="tablist">
          <li class="nav-item mr-2 mt-1 mb-1" role="presentation">
            <a class="nav-link active" id="pills-tab1" data-toggle="pill" href="#pills-home" role="tab" aria-controls="pills-home" aria-selected="true">歷史開獎紀錄</a>
          </li>
          <li class="nav-item mr-2 mt-1 mb-1" role="presentation">
            <a class="nav-link" id="pills-tab2" data-toggle="pill" href="#pills-profile" role="tab" aria-controls="pills-profile" aria-selected="false">超級獎號走勢</a>
          </li>
          <li class="nav-item mr-2 mt-1 mb-1" role="presentation">
            <a class="nav-link" id="pills-tab3" data-toggle="pill" href="#pills-contact" role="tab" aria-controls="pills-contact" aria-selected="false">冷熱碼</a>
          </li>
        </ul>
        <div class="tab-content" id="pills-tabContent">
          <!-- 歷史開獎紀錄 -->
          <div class="overflow-auto tab-pane fade show active" id="pills-home" role="tabpanel" aria-labelledby="pills-tab1">
            <table class="table table-striped tableList">
              <thead>
                <tr>
                  <th class="align-middle" scope="col">期別</th>
                  <th class="align-middle" scope="col">開獎號碼</th>
                  <th class="align-middle" scope="col">超級獎號</th>
                  <th class="align-middle" scope="col">獎號總和</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(items, i) in historyList" :key="i">
                  <td class="align-middle font-weight-bold">
                    <div class="w-130">
                      第{{ items.number }}期
                    </div>
                  </td>
                  <td class="align-middle">
                    <div class="d-flex justify-content-center">
                      <div class="ball w-320">
                        <div :class="['defaultBall blackTextBall', {'specialBall': ball === items.superBall}]" v-for="ball in items.balls.split(',')">{{ ball }}</div>
                      </div>

                      <!-- <div class="ball w-320">
                        <div class="defaultBall blackTextBall">01</div>
                        <div class="defaultBall blackTextBall">02</div>
                        <div class="defaultBall blackTextBall specialBall">03</div>
                        <div class="defaultBall blackTextBall">04</div>
                        <div class="defaultBall blackTextBall">05</div>
                        <div class="defaultBall blackTextBall">06</div>
                        <div class="defaultBall blackTextBall">07</div>
                        <div class="defaultBall blackTextBall">08</div>
                        <div class="defaultBall blackTextBall">09</div>
                        <div class="defaultBall blackTextBall">10</div>
                        <div class="defaultBall blackTextBall">11</div>
                        <div class="defaultBall blackTextBall">12</div>
                        <div class="defaultBall blackTextBall">13</div>
                        <div class="defaultBall blackTextBall">14</div>
                        <div class="defaultBall blackTextBall">15</div>
                        <div class="defaultBall blackTextBall">16</div>
                        <div class="defaultBall blackTextBall">17</div>
                        <div class="defaultBall blackTextBall">18</div>
                        <div class="defaultBall blackTextBall">19</div>
                        <div class="defaultBall blackTextBall">20</div>
                      </div> -->
                    </div>
                  </td>
                  <td class="align-middle font-weight-bold">
                    <div class="d-flex justify-content-center">
                      <div class="superBall">
                        {{ items.superBall }}
                      </div>
                    </div>
                  </td>
                  <td class="align-middle font-weight-bold">
                    <div class="d-flex justify-content-center">
                      <div class="totalBall text-primary">
                        {{ items.totalBalls }}
                      </div>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- 超級獎號走勢 -->
          <div class="tab-pane fade" id="pills-profile" role="tabpanel" aria-labelledby="pills-tab2">
            <div class="mb-3">
              <canvas id="superBallChart"></canvas>
            </div>
          </div>

          <!-- 冷熱碼 -->
          <div class="overflow-auto tab-pane fade" id="pills-contact" role="tabpanel" aria-labelledby="pills-tab3">
            <table class="table table-striped tableList">
              <tbody>
                <tr v-for="(items, i) in hotBalls" :key="i">
                  <td class="align-middle" v-for="(content, j) in items" :key="j">
                    <div class="ball float-left">
                      <div class="defaultBall blackTextBall">{{ content.ball }}</div>
                    </div>
                    <div class="pt-1">
                      {{ content.count }}次
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </main>

    <footer></footer>

    <a href="#" class="toTop" title="GoTop" style="display: inline;"><span></span></a>
  </div>
</template>

<script>
import $ from 'jquery'
import Chart from 'chart.js'

export default {
  name: 'BingoHome',
  data () {
    return {
      // 歷史開獎紀錄列表
      historyList: [
        { number: '000000001', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '10', totalBalls: '210' },
        { number: '000000002', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '05', totalBalls: '210' },
        { number: '000000003', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '13', totalBalls: '210' },
        { number: '000000004', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '20', totalBalls: '210' },
        { number: '000000005', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '17', totalBalls: '210' },
        { number: '000000006', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '03', totalBalls: '210' },
        { number: '000000007', balls: '01,02,03,04,05,06,07,08,09,10,41,42,43,44,45,46,47,48,49,50', superBall: '44', totalBalls: '210' },
        { number: '000000008', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '10', totalBalls: '210' },
        { number: '000000009', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '04', totalBalls: '210' },
        { number: '000000010', balls: '11,12,13,14,15,16,17,18,19,20,31,32,33,34,35,36,37,38,39,40', superBall: '31', totalBalls: '210' }
      ],
      // 冷熱碼列表
      hotBalls: [
        [
          {ball: '01', count: '0'},{ball: '02', count: '0'},{ball: '03', count: '0'},{ball: '04', count: '0'},{ball: '05', count: '95'},
          {ball: '06', count: '0'},{ball: '07', count: '100'},{ball: '08', count: '0'},{ball: '09', count: '0'},{ball: '10', count: '98'}
        ],
        [
          {ball: '11', count: '0'},{ball: '12', count: '0'},{ball: '13', count: '0'},{ball: '14', count: '0'},{ball: '15', count: '0'},
          {ball: '16', count: '0'},{ball: '17', count: '0'},{ball: '18', count: '0'},{ball: '19', count: '0'},{ball: '20', count: '102'}
        ],
        [
          {ball: '21', count: '0'},{ball: '22', count: '0'},{ball: '23', count: '0'},{ball: '24', count: '0'},{ball: '25', count: '0'},
          {ball: '26', count: '0'},{ball: '27', count: '0'},{ball: '28', count: '0'},{ball: '29', count: '0'},{ball: '30', count: '0'}
        ],
        [
          {ball: '31', count: '0'},{ball: '32', count: '0'},{ball: '33', count: '0'},{ball: '34', count: '0'},{ball: '35', count: '0'},
          {ball: '36', count: '0'},{ball: '37', count: '0'},{ball: '38', count: '0'},{ball: '39', count: '0'},{ball: '40', count: '0'}
        ],
        [
          {ball: '41', count: '0'},{ball: '42', count: '0'},{ball: '43', count: '0'},{ball: '44', count: '0'},{ball: '45', count: '0'},
          {ball: '46', count: '0'},{ball: '47', count: '0'},{ball: '48', count: '0'},{ball: '49', count: '0'},{ball: '50', count: '0'}
        ],
        [
          {ball: '51', count: '0'},{ball: '52', count: '0'},{ball: '53', count: '0'},{ball: '54', count: '0'},{ball: '55', count: '0'},
          {ball: '56', count: '0'},{ball: '57', count: '0'},{ball: '58', count: '0'},{ball: '59', count: '0'},{ball: '60', count: '0'}
        ],
        [
          {ball: '61', count: '0'},{ball: '62', count: '0'},{ball: '63', count: '0'},{ball: '64', count: '0'},{ball: '65', count: '0'},
          {ball: '66', count: '0'},{ball: '67', count: '0'},{ball: '68', count: '0'},{ball: '69', count: '0'},{ball: '70', count: '0'}
        ],
        [
          {ball: '71', count: '0'},{ball: '72', count: '0'},{ball: '73', count: '0'},{ball: '74', count: '0'},{ball: '75', count: '0'},
          {ball: '76', count: '0'},{ball: '77', count: '0'},{ball: '78', count: '0'},{ball: '79', count: '0'},{ball: '80', count: '50'}
        ]
      ]
    }
  },
  mounted () {
    this.setChart()
    this.setGoToTop()
  },
  methods: {
    setChart () {
      var ctx2 = document.getElementById('superBallChart')
      var superBallChart = new Chart(ctx2, {
        // 屬性表示圖形形狀
        type: 'line',
        // 屬性配置圖形上的數據，data裏的數據可以參考各個type的圖每個參數的說明
        data: {
          // X軸數值
          labels: [
                    '95', '96', '97', '98', '99', '00', '01', '02', '03', '04',
                    '05', '06', '07', '08', '09', '10', '11', '12', '13', '14',
                    '15', '16', '17', '18', '19', '20', '21', '22', '23', '24',
                    '25', '26', '27', '28', '29', '30', '31', '32', '33', '34'
                  ],
          datasets: [
            {
              label: '超級獎號',
              backgroundColor: '#057eff',
              borderColor: '#057eff',
              borderWidth: 3,
              pointStrokeColor: '#fff',
              pointStyle: 'crossRot',
              // 資料內容
              data: [
                25, 39, 0, 21, 46, 10, 40, 52, 32, 24, 10, 10,
                25, 39, 0, 21, 46, 10, 40, 22, 32, 24, 10, 3,
                25, 39, 77, 21, 46, 10, 50, 22, 32, 24, 10, 1,
                25, 39, 0, 21, 46, 10, 40, 22, 32, 24, 10, 63
              ],
              cubicInterpolationMode: 'monotone',
              spanGaps: 'false',
              fill: 'false',
              radius: 3,
              pointStyle: 'circle'
            }
          ]
        },
        // 配置圖形其他的可選項
        options: {
          legend: {
            // 顯示或隱藏圖例
            display: false,
            labels: {}
          },
          scales: {
            // Y軸設定
            yAxes: [
              {
                stacked: true,
                ticks: {
                  suggestedMin: 0,
                  suggestedMax: 80
                }
              }
            ]
          }
        }
      })
    },
    setGoToTop () {
      // gotop
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
    }
  }
}
</script>

<style lang="scss" scoped>
.tinyBingo {
  /* 當前資訊區 */
  .currentInfo {
    padding: 16px 0 10px 0;
    border-radius: 4px;
    background-color: #f6f9fa;
    p {
      color: #212736;
      font-weight: bold;
    }

    // 倒數器
    .countdown {
      .time {
        float: left;
        width: 54px;
        height: 60px;
        border-radius: 8px;
        box-shadow: 1px 1px 4px 0 rgba(80, 80, 80, 0.5);
        background-color: #919aa3;
        padding: 5px;
        font-size: 36px;
        color: #ffffff;
      }
      .timeColon {
        font-size: 36px;
        padding: 0px 4px 0px 4px;
        color: #919aa3;
      }
    }

    // 當期球號
    .currentNumber {}

    // 超級獎號
    .superBall {
      width: 80px;
      height: 80px;
      padding: 8px;
      border: solid 4px #dedede;
      border-radius: 50%;
      background-image: linear-gradient(to bottom, #ff4e4e 1%, #d70a0a);
      color: #fff;
      font-size: 40px;
      margin: 0 auto;
    }

    // 獎號總和
    .totalBall {
      padding: 10px;
      font-size: 40px;
      color: #029fff;
    }
  }

  /* 預測資訊區 */
  .predictionInfo {
    padding: 10px;
    border-radius: 4px;
    background-color: #ffefef;
    .predictionNumber {
      color: #ff4e4e;
      font-weight: 500;
    }
  }

  /* 分頁分析區 */
  .nav-pills .nav-link.active {
    border-radius: 20px;
    color: #54a0e5;
    background-color: #e1efff;
  }
  .nav-item {
    border-radius: 20px;
    color: #919aa3;
    background-color: #f0f4f7;
    a {
      color: #919aa3;
    }
  }
  // 表格
  .tableList {
    // 超級獎號
    .superBall {
      width: 50px;
      height: 50px;
      padding: 8px;
      border: solid 3px #dedede;
      border-radius: 50%;
      background-color: #ffabab;
      color: #151515;
      font-size: 20px;
    }
    // 獎號總和
    .totalBall {
      padding: 10px;
      font-size: 20px;
    }
  }

  /* gototop */
  .toTop span {
    position: fixed;
    bottom: 70px;
    right: 24px;
    opacity: .9;
    height: 50px;
    width: 50px;
    border-radius: 50%;
    text-align: center;
    background: #54a0e5;
    box-shadow: 1px 1px 4px 0 rgb(2, 46, 93);
    line-height: 45px;
    z-index: 9
  }
  .toTop span:hover {
    background: #057eff
  }
  .toTop span::before {
    content: "";
    position: absolute;
    left: calc(50% - 7.5px);
    top: calc(50% - 14px);
    width: 0;
    height: 15px;
    border: 7px solid transparent;
    border-top: 10px solid #f6f6f6;
    transform: rotate(180deg)
  }

  /* 共用 */
  // 球號
  .ball {
    .defaultBall {
      display: inline-block;
      width: 26px;
      height: 26px;
      margin: 2px 5px 2px 0px;
      border-radius: 50%;
      line-height: 26px;
      text-align: center;
      font-weight: 500;
      color: #fff;
      background-color: #ffb14e;
    }
    // 預設超級獎號
    .defaultBall.specialBall {
      background-color: #ff4e4e;
    }
    // 黑色文字球號
    .blackTextBall {
      color: #151515;
      background-color: #ffd196;
    }
    // 黑色文字超級獎號
    .blackTextBall.specialBall {
      background-color: #ffabab;
    }
  }

  // 寬度
  .w-320 {
    width: 320px;
  }
  .w-130 {
    width: 130px;
  }

  // bootstrap表格覆蓋樣式
  .table {
    border: 1px solid #ebeef1;
  }
  .table td {
    border-bottom: 1px solid #ebeef1;
  }
  .table td, .table th {
    border-top: unset;
  }
  .table thead th {
    background-color: #f1f3f6;
    color: #919aa3;
    border-bottom: 1px solid #ebeef1;
  }
  .table-striped tbody tr:nth-of-type(odd){
    background-color: #ffffff;
  }
  .table-striped tbody tr:nth-of-type(even){
    background-color: #fbfcfc;
  }

  @media (max-width:992px) {
    .predictionInfo .d-flex {
      display: unset !important;
    }
  }
}
</style>
