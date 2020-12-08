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
            <div class="countdown col-md-4 col-sm-12 pb-3">
              <p>距離下期開獎剩餘</p>
              <div class="d-flex justify-content-center text-center">
                <span class="timeMinutes">
                  03
                </span>
                <span class="timeColon">:</span>
                <span class="timeSeconds">
                  56
                </span>
              </div>
            </div>

            <!-- 當前期號 -->
            <div class="currentNumber col-md-4 col-sm-12 pb-3 text-md-left text-sm-center">
              <p>第<span>000000005</span>期</p>
              <div class="ball">
                <div class="whiteNumber">01</div>
                <div class="whiteNumber">02</div>
                <div class="whiteNumber">03</div>
                <div class="whiteNumber">04</div>
                <div class="whiteNumber">05</div>
                <div class="whiteNumber">06</div>
                <div class="whiteNumber">07</div>
                <div class="whiteNumber">08</div>
                <div class="whiteNumber">09</div>
                <div class="whiteNumber">10</div>
                <div class="whiteNumber">11</div>
                <div class="whiteNumber">12</div>
                <div class="whiteNumber">13</div>
                <div class="whiteNumber">14</div>
                <div class="whiteNumber">15</div>
                <div class="whiteNumber">16</div>
                <div class="whiteNumber">17</div>
                <div class="whiteNumber">18</div>
                <div class="whiteNumber">19</div>
                <div class="whiteNumber superNumber">20</div>
              </div>
            </div>

            <!-- 超級獎號 -->
            <div class="col-md-2 col-sm-6 pb-3">
              <p>超級獎號</p>
              <div class="d-flex justify-content-center text-center">
                <div class="superBall">
                  20
                </div>
              </div>
            </div>

            <!-- 獎號總和 -->
            <div class="col-md-2 col-sm-6">
              <p>獎號總和</p>
              <div class="d-flex justify-content-center text-center">
                <div class="totalBall text-primary">
                  210
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- 預測資訊區 -->
        <div class="predictionInfo mt-3 text-left d-flex align-items-center">
          <span class="predictionNumber">000000006期預測總和 小</span>
          <span class="ball ml-4">
            <div class="blackNumber">01</div>
            <div class="blackNumber">02</div>
            <div class="blackNumber">03</div>
            <div class="blackNumber">04</div>
            <div class="blackNumber">05</div>
            <div class="blackNumber">06</div>
            <div class="blackNumber">07</div>
            <div class="blackNumber superNumber">08</div>
            <div class="blackNumber">09</div>
            <div class="blackNumber">10</div>
            <div class="blackNumber">11</div>
            <div class="blackNumber">12</div>
            <div class="blackNumber">13</div>
            <div class="blackNumber">14</div>
            <div class="blackNumber">15</div>
            <div class="blackNumber">16</div>
            <div class="blackNumber">17</div>
            <div class="blackNumber">18</div>
            <div class="blackNumber">19</div>
            <div class="blackNumber">20</div>
          </span>
        </div>

        <!-- 分頁分析區 -->
        <ul class="nav nav-pills mt-3 mb-3" id="pills-tab" role="tablist">
          <li class="nav-item mr-2" role="presentation">
            <a class="nav-link active" id="pills-tab1" data-toggle="pill" href="#pills-home" role="tab" aria-controls="pills-home" aria-selected="true">歷史開獎紀錄(1)</a>
          </li>
          <li class="nav-item mr-2" role="presentation">
            <a class="nav-link" id="pills-tab2" data-toggle="pill" href="#pills-profile" role="tab" aria-controls="pills-profile" aria-selected="false">超級獎號走勢(1)</a>
          </li>
          <li class="nav-item mr-2" role="presentation">
            <a class="nav-link" id="pills-tab3" data-toggle="pill" href="#pills-contact" role="tab" aria-controls="pills-contact" aria-selected="false">冷熱碼(1)</a>
          </li>
        </ul>
        <div class="tab-content" id="pills-tabContent">
          <!-- 歷史開獎紀錄 -->
          <div class="tab-pane fade show active" id="pills-home" role="tabpanel" aria-labelledby="pills-tab1">
            <table class="table table-striped tableList">
              <thead>
                <tr>
                  <th scope="col">期別</th>
                  <th scope="col">開獎號碼</th>
                  <th scope="col">超級獎號</th>
                  <th scope="col">獎號總和</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(items, i) in historyList" :key="i">
                  <td class="align-middle">第{{ items.number }}期</td>
                  <td class="align-middle">
                    <!-- <div class="ball">
                      <div class="blackNumber">01</div>
                      <div class="blackNumber">02</div>
                      <div class="blackNumber superNumber">03</div>
                      <div class="blackNumber">04</div>
                      <div class="blackNumber">05</div>
                      <div class="blackNumber">06</div>
                      <div class="blackNumber">07</div>
                      <div class="blackNumber">08</div>
                      <div class="blackNumber">09</div>
                      <div class="blackNumber">10</div>
                      <div class="blackNumber">11</div>
                      <div class="blackNumber">12</div>
                      <div class="blackNumber">13</div>
                      <div class="blackNumber">14</div>
                      <div class="blackNumber">15</div>
                      <div class="blackNumber">16</div>
                      <div class="blackNumber">17</div>
                      <div class="blackNumber">18</div>
                      <div class="blackNumber">19</div>
                      <div class="blackNumber">20</div>
                    </div> -->
                    <div class="ball">
                      <div :class="['blackNumber', {'superNumber': ball === items.superBall}]" v-for="ball in items.balls.split(',')">{{ ball }}</div>
                    </div>
                  </td>
                  <td class="align-middle">
                    <div class="superBall">
                      {{ items.superBall }}
                    </div>
                  </td>
                  <td class="align-middle">
                    <div class="totalBall text-primary">
                      {{ items.totalBalls }}
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- 超級獎號走勢 -->
          <div class="tab-pane fade" id="pills-profile" role="tabpanel" aria-labelledby="pills-tab2">
            .....
          </div>

          <!-- 冷熱碼 -->
          <div class="tab-pane fade" id="pills-contact" role="tabpanel" aria-labelledby="pills-tab3">
            <table class="table table-striped tableList">
              <tbody>
                <tr v-for="(items, i) in hotBalls" :key="i">
                  <td v-for="(content, j) in items" :key="j">
                    <div class="ball"><div class="blackNumber">{{ content.ball }}</div></div>
                    <div class="">{{ content.count }}次</div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </main>

    <footer></footer>
  </div>
</template>

<script>
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
        { number: '000000005', balls: '01,02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,18,19,20', superBall: '17', totalBalls: '210' }
      ],
      // 冷熱碼列表
      hotBalls: [
        [
          {ball: '01', count: '27'},{ball: '02', count: '27'},{ball: '03', count: '27'},{ball: '04', count: '27'},{ball: '05', count: '27'},
          {ball: '06', count: '27'},{ball: '07', count: '27'},{ball: '08', count: '27'},{ball: '09', count: '27'},{ball: '10', count: '27'}
        ],
        [
          {ball: '11', count: '27'},{ball: '12', count: '27'},{ball: '13', count: '27'},{ball: '14', count: '27'},{ball: '15', count: '27'},
          {ball: '16', count: '27'},{ball: '17', count: '27'},{ball: '18', count: '27'},{ball: '19', count: '27'},{ball: '20', count: '27'}
        ],
        [
          {ball: '21', count: '27'},{ball: '22', count: '27'},{ball: '23', count: '27'},{ball: '24', count: '27'},{ball: '25', count: '27'},
          {ball: '26', count: '27'},{ball: '27', count: '27'},{ball: '28', count: '27'},{ball: '29', count: '27'},{ball: '30', count: '27'}
        ],
        [
          {ball: '31', count: '27'},{ball: '32', count: '27'},{ball: '33', count: '27'},{ball: '34', count: '27'},{ball: '35', count: '27'},
          {ball: '36', count: '27'},{ball: '37', count: '27'},{ball: '38', count: '27'},{ball: '39', count: '27'},{ball: '40', count: '27'}
        ],
        [
          {ball: '41', count: '27'},{ball: '42', count: '27'},{ball: '43', count: '27'},{ball: '44', count: '27'},{ball: '45', count: '27'},
          {ball: '46', count: '27'},{ball: '47', count: '27'},{ball: '48', count: '27'},{ball: '49', count: '27'},{ball: '50', count: '27'}
        ],
        [
          {ball: '51', count: '27'},{ball: '52', count: '27'},{ball: '53', count: '27'},{ball: '54', count: '27'},{ball: '55', count: '27'},
          {ball: '56', count: '27'},{ball: '57', count: '27'},{ball: '58', count: '27'},{ball: '59', count: '27'},{ball: '60', count: '27'}
        ],
        [
          {ball: '61', count: '27'},{ball: '62', count: '27'},{ball: '63', count: '27'},{ball: '64', count: '27'},{ball: '65', count: '27'},
          {ball: '66', count: '27'},{ball: '67', count: '27'},{ball: '68', count: '27'},{ball: '69', count: '27'},{ball: '70', count: '27'}
        ],
        [
          {ball: '71', count: '27'},{ball: '72', count: '27'},{ball: '73', count: '27'},{ball: '74', count: '27'},{ball: '75', count: '27'},
          {ball: '76', count: '27'},{ball: '77', count: '27'},{ball: '78', count: '27'},{ball: '79', count: '27'},{ball: '80', count: '27'}
        ]
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.tinyBingo {
  /* 當前資訊區 */
  .currentInfo {
    padding: 20px;
    border-radius: 4px;
    background-color: #f6f9fa;
    p {
      color: #212736;
      font-weight: bold;
    }

    // 倒數器
    .countdown {
      .timeMinutes,
      .timeSeconds {
        float: left;
        width: 54px;
        height: 60px;
        border-radius: 8px;
        box-shadow: 1px 1px 4px 0 rgba(80, 80, 80, 0.5);
        background-color: #919aa3;
        padding: 5px;
        font-family: Arial;
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
    .currentNumber {
      // 球號
      // .ball div {
      //   float: left;
      //   width: 28px;
      //   height: 28px;
      //   color: #fff;
      //   margin: 0px 5px 5px 0px;
      //   border-radius: 50%;
      //   background-color: #ffb14e;
      //   line-height: 28px;
      //   text-align: center;
      // }
    }
    // 超級獎號
    .superBall {
      width: 80px;
      height: 80px;
      padding: 8px;
      border: solid 4px #dedede;
      border-radius: 50%;
      background-image: linear-gradient(to bottom, #ff4e4e 1%, #d70a0a);
      color: #fff;
      font-size: 38px;
    }
    // 獎號總和
    .totalBall {
      padding: 10px;
      font-family: Arial;
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
    }
    // 球號
    // .ball div {
    //   float: left;
    //   width: 28px;
    //   height: 28px;
    //   color: #fff;
    //   margin: 0px 2px;
    //   border-radius: 50%;
    //   background-color: #ffb14e;
    //   line-height: 28px;
    //   text-align: center;
    // }
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
  .tableList {
    // 開獎號碼
    // .ball div {
    //   float: left;
    //   width: 28px;
    //   height: 28px;
    //   color: #fff;
    //   margin: 0px 5px 5px 0px;
    //   border-radius: 50%;
    //   background-color: #ffb14e;
    //   line-height: 28px;
    //   text-align: center;
    // }
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
      font-family: Arial;
      font-size: 20px;
    }
  }

  // 球號
  .ball {
    div {
      float: left;
      width: 28px;
      height: 28px;
      margin: 0px 5px 5px 0px;
      border-radius: 50%;
      line-height: 1.9;
      text-align: center;
    }
    // 白色文字球號
    .whiteNumber {
      color: #fff;
      background-color: #ffb14e;
    }
    // 白色文字超級獎號
    .whiteNumber.superNumber {
      background-color: #ff4e4e;
    }
    // 黑色文字球號
    .blackNumber {
      color: #151515;
      background-color: #ffd196;
    }
    // 黑色文字超級獎號
    .blackNumber.superNumber {
      background-color: #ffabab;
    }
  }
}
</style>
