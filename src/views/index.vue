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
        <div class="font-weight-bold mb-3">第123456789期</div>
          <ul class="nav mb-1 d-flex justify-content-center">
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay special-number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
          </ul>
          <ul class="nav d-flex justify-content-center">
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
            <li class="number-inplay">11</li>
          </ul>
      </div>

      <div class="col-sm-2">
        <div class="font-weight-bold mb-2">超級獎號</div>
        <div class="Oval">
          <div class="super-number">45</div>
        </div>
      </div>
      <div class="col-sm-2">
        <div class="font-weight-bold mb-3">獎號總和</div>
        <div class="text-primary number-total font-weight-bold">118</div>
      </div>
    </div>

    <!-- 第二塊預期總和 -->
    <div class="lottery-numbers-bg mb-3">
      <div class="text-left float-left lottery-text font-weight-bold">109067899898期預測總和 小</div>
        <ul class="nav">
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers special-number">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
          <li class="number-inplay lottery-numbers">11</li>
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
          <div>
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
                <tr>
                  <td class="font-weight-bold period">第111111111期</td>
                  <td>
                    <ul class="nav mb-1 d-flex justify-content-center">
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers special-number-inplay">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                    </ul>
                    <ul class="nav d-flex justify-content-center">
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                    </ul>
                  </td>
                  <td>
                    <div class="history-special-number">45</div>
                  </td>
                  <td><div class="history-number-total">118</div></td>
                </tr>
                <tr>
                  <td class="font-weight-bold period">第222222222期</td>
                  <td>
                    <ul class="nav mb-1 d-flex justify-content-center">
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers special-number-inplay">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                    </ul>
                    <ul class="nav d-flex justify-content-center">
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                    </ul>
                  </td>
                  <td>
                    <div class="history-special-number">45</div>
                  </td>
                  <td><div class="history-number-total">118</div></td>
                </tr>
                <tr>
                  <td class="font-weight-bold period">第333333333期</td>
                  <td>
                    <ul class="nav mb-1 d-flex justify-content-center">
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers special-number-inplay">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                    </ul>
                    <ul class="nav d-flex justify-content-center">
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                      <li class="number-inplay lottery-numbers">11</li>
                    </ul>
                  </td>
                  <td>
                    <div class="history-special-number">45</div>
                  </td>
                  <td><div class="history-number-total">118</div></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- 超級開獎號碼 -->
        <div class="tab-pane fade" id="pills-super" role="tabpanel" aria-labelledby="pills-super-tab">
          <div class="super-tab-bg">
            <div style="height:350px">
              走勢圖在這！
            </div>
          </div>
        </div>
        <!-- 冷熱碼 -->
        <div class="tab-pane fade" id="pills-hot" role="tabpanel" aria-labelledby="pills-hot-tab">

        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>

</script>

<style>


</style>