<script setup>
import { ref } from "vue";
import one from "../src/assets/widthlong1.png";
import two from "../src/assets/widthlong2.png";
import three from "../src/assets/widthlong3.png";
import four from "../src/assets/widthlong4.png";
import five from "../src/assets/widthlong5.png";

const imgs = ref([one, two, three, four, five]);

// showCarousel 代表從第0張開始
const showCarousel = ref(0);

// 綁訂在 TransitionGroup name 預設是 listLeft
const transitionName = ref("listLeft");

const buttonState = ref(false);

// 按下按鈕時，先將 buttonState 設為 true，一段時間後再設回 false
function buttonDisabled() {
  buttonState.value = true;
  setTimeout(() => (buttonState.value = false), 2100);
}

// 按上一張到小於0=>從左邊進來
// 按下一張到大於總長度=>從右邊進來
function setShowCarousel(index) {
  if (index < 0) {
    // 按上一張到小於0-->從左邊進來
    buttonDisabled();
    transitionName.value = "listLeft";
    showCarousel.value = imgs.value.length - 1;
  } else if (index > imgs.value.length - 1) {
    // 按下一張到大於總長度-->從右邊進來
    buttonDisabled();
    showCarousel.value = 0;
    transitionName.value = "listRight";
  } else {
    buttonDisabled();
    // 決定播放哪種過場動畫 條件: 目前第幾張,是否小於總數 成立:從右邊進來 不成立:從左邊進來
    transitionName.value =
      showCarousel.value < index ? "listRight" : "listLeft";
    showCarousel.value = index;
    // 顯示指定的圖片
  }
}

// intervalId 會被用來存放 setInterval 函數所返回的計時器ID，以便於之後停止計時器。
let intervalId = null;

// // 啟動自動播放功能
function startCarousel() {
  intervalId = setInterval(function () {
    if (showCarousel.value > imgs.value.length - 2) {
      showCarousel.value = -1;
    }
    showCarousel.value++;
  }, 3000);
}

startCarousel();

// 停止自動播放功能
function stopCarousel() {
  clearInterval(intervalId);
}
</script>

<template>
  <section>
    <button
      @mouseenter="stopCarousel"
      @mouseleave="startCarousel"
      @click="setShowCarousel(showCarousel - 1)"
      :disabled="buttonState"
      class="carouselLeft"
    >
      ⇦
    </button>

    <button
      @mouseenter="stopCarousel"
      @mouseleave="startCarousel"
      @click="setShowCarousel(showCarousel + 1)"
      :disabled="buttonState"
      class="carouselRight"
    >
      ⇨
    </button>

    <div class="carouselSection">
      <transition-group
        :name="transitionName"
        tag="div"
        class="carouselContainer"
      >
        <ul
          @mouseenter="stopCarousel"
          @mouseleave="startCarousel"
          class="page"
          v-for="(img, index) in imgs"
          :key="index"
          v-show="index == showCarousel"
        >
          <li><img class="pageImg" :src="img" /></li>
          <li><img class="pageImgPOA" :src="img" /></li>
        </ul>
      </transition-group>
    </div>
    <div class="carouselOneToFive">
      <button
        @mouseenter="stopCarousel"
        @mouseleave="startCarousel"
        @click="buttonDisabled(), (showCarousel = 0)"
        :disabled="buttonState"
        class="mar5"
      >
        ○
      </button>
      <button
        @mouseenter="stopCarousel"
        @mouseleave="startCarousel"
        @click="buttonDisabled(), (showCarousel = 1)"
        :disabled="buttonState"
        class="mar5"
      >
        ○
      </button>
      <button
        @mouseenter="stopCarousel"
        @mouseleave="startCarousel"
        @click="buttonDisabled(), (showCarousel = 2)"
        :disabled="buttonState"
        class="mar5"
      >
        ○
      </button>
      <button
        @mouseenter="stopCarousel"
        @mouseleave="startCarousel"
        @click="buttonDisabled(), (showCarousel = 3)"
        :disabled="buttonState"
        class="mar5"
      >
        ○
      </button>
      <button
        @mouseenter="stopCarousel"
        @mouseleave="startCarousel"
        @click="buttonDisabled(), (showCarousel = 4)"
        :disabled="buttonState"
        class="mar5"
      >
        ○
      </button>
    </div>
  </section>
  <section>
    <div class="disCen">
      <div class="readMeCard">
        <div class="fz24">您好，歡迎來到 Wayne Lu 的輪播 project</div>
        <br />
        <div class="top10">
          這個輪播功能使用 html + css + JavaScript + Vue 製作而成
        </div>
        <div class="top10">
          先在 ul 做v-for="(img, index) in imgs"將 5 個 li 標籤引入圖片 imgs
        </div>

        <div class="bgcVS">
          <div>
            <span class="function">const</span> <span class="word">imgs</span>
            <span class="then">=</span> <span class="variable">ref</span>
            <span class="brackets">([</span> <span class="word">one,</span>
            <span class="word">two,</span> <span class="word">three,</span>
            <span class="word">four,</span> <span class="word">five</span>
            <span class="brackets">])</span> <span class="then">;</span>
          </div>
          <div>
            <span class="then">˂</span> <span class="number">div</span>
            <span class="then">˃</span>
          </div>
          <div class="pTwo">
            <span class="then">˂</span><span class="number">ul </span>
            <span class="then">v-for="</span> <span class="brackets">(</span>
            <span class="word">img,</span> <span class="word">index</span>
            <span class="brackets">)</span> <span class="then">in </span>
            <span class="word">imgs</span> <span class="then">" :</span>
            <span class="function">key</span> <span class="then">="</span>
            <span class="word">index</span><span class="then">" </span>
            <span class="function">v-show</span> <span class="then">="</span>
            <span class="word">index</span> <span class="then">==</span>
            <span class="word">showCarousel</span> <span class="then">"˃</span>
          </div>
          <div class="pFou">
            <span class="then">˂</span> <span class="number">li</span>
            <span class="then">˃˂</span> <span class="number">img</span>
            <span class="then"> :</span><span class="function">src</span>
            <span class="then">="</span> <span class="word">img</span>
            <span class="then">"/˃˂/</span> <span class="number">li</span>
            <span class="then">˃</span>
          </div>
          <div class="pTwo">
            <span class="then">˂/</span> <span class="number">ul</span>
            <span class="then">˃</span>
          </div>
          <div>
            <span class="then">˂/</span> <span class="number">div</span>
            <span class="then">˃</span>
          </div>
        </div>

        <div class="top10">目標是先用一個 div 將這個 ul 列表包起來</div>
        <div class="top10">在這個 div 加上 position: relative</div>
        <div class="top10">讓這 5 張圖片重疊在同一位置</div>
        <div class="top10">
          宣告一個 showCarousel = ref(0) 的 ref 值 (代表從第0張開始)
        </div>
        <div class="top10">
          利用 v-show="index == showCarousel" 來決定目前要顯示第幾張
        </div>
        <div class="top10">
          再來宣告 startCarousel 函式將 showCarousel.value++
        </div>
        <div class="top10">另外對 showCarousel 加上了 if 判斷式</div>
        <div class="top10">
          判斷邏輯 : 當我目前要顯示第幾張 大於 我引入圖片的長度
        </div>
        <div class="top10 pFou">
          要顯示第一張的前一張 (showCarousel.value = -1)
        </div>
        <div class="top10 pFou">之後做 showCarousel.value++</div>
        <br />

        <div class="bgcVS">
          <div>
            <span class="function">let </span>
            <span class="word">intervalId</span> <span class="then">= </span>
            <span class="then">null;</span>
          </div>
          <div>
            <span class="function">const </span>
            <span class="word">showCarousel</span> <span class="then">= </span>
            <span class="variable">ref</span> <span class="brackets">(</span>
            <span class="number">0</span> <span class="brackets">)</span>
            <span class="then">;</span>
          </div>
          <div>
            <span class="function">function </span>
            <span class="word">startCarousel</span>
            <span class="brackets">() {</span>
          </div>
          <div class="pTwo">
            <span class="word">intervalId</span> <span class="then">= </span>
            <span class="word">setInterval</span>
            <span class="brackets">(</span>
            <span class="function">function</span>
            <span class="brackets">(){</span>
          </div>
          <div class="pFou">
            <span class="then">if</span> <span class="brackets">(</span>
            <span class="word">showCarousel.value </span>
            <span class="then">> </span>
            <span class="word">imgs.value.length </span>
            <span class="then">-</span> <span class="number">2</span>
            <span class="brackets">) {</span>
          </div>
          <div class="pSix">
            <span class="word">showCarousel.value</span>
            <span class="then">= -</span> <span class="number">1</span>
            <span class="then">;</span>
          </div>
          <div class="pFou">
            <span class="brackets">}</span>
          </div>
          <div class="pFou">
            <span class="word">showCarousel.value</span>
            <span class="then">++;</span>
          </div>
          <div class="pTwo">
            <span class="brackets">}</span> <span class="then">,</span>
            <span class="number">3000</span> <span class="brackets">)</span>
            <span class="then">;</span>
          </div>
          <span class="brackets">}</span>
        </div>

        <div class="top10">再加上 transition-group 而達到輪播的功能</div>
        <div class="top10">另外加上了 setShowCarousel 對 index 值做判斷式</div>
        <div class="top10">判斷邏輯 : 當按往左按鈕要動畫從左邊進來</div>
        <div class="top10 pFou">
          如果按到 index ˂ 0 要將 showCarousel 設定到最後一張
        </div>
        <div class="top10 pFou">當按往左按鈕要動畫從右邊進來</div>
        <div class="top10 pFou">
          如果按到 index > 最後一張 要將 showCarousel 設定到第一張
        </div>
        <br />
        <div class="bgcVS">
          <div>
            <span class="function">function </span>
            <span class="variable">setShowCarousel</span
            ><span class="brackets">(</span><span class="word">index</span>
            <span class="brackets">){</span>
          </div>
          <div class="pTwo">
            <span class="then">if</span> <span class="brackets">(</span>
            <span class="word">index</span> <span class="then">˂</span>
            <span class="number">0</span> <span class="brackets">){</span>
          </div>
          <div class="pFou">
            <span class="word">transitionName.value</span>
            <span class="then">=</span> <span class="then">"</span>
            <span class="src">listLeft</span> <span class="then">";</span>

            <span class="comment"> //按上一張到小於0->從左邊進來</span>
          </div>
          <div class="pFou">
            <span class="word">showCarousel.value</span>
            <span class="then">=</span>
            <span class="word">imgs.value.length </span>
            <span class="then">-</span> <span class="number">1</span>
            <span class="then">;</span>
          </div>
          <div class="pTwo">
            <span class="brackets">}</span> <span class="then">else if </span>
            <span class="brackets">(</span> <span class="word">index </span>
            <span class="then">> </span>
            <span class="word">imgs.value.length </span>
            <span class="then">-</span> <span class="number">1</span>
            <span class="brackets">){ </span>
          </div>
          <div class="pFou">
            <span class="word">showCarousel.value </span>
            <span class="then">=</span> <span class="number">0</span>
            <span class="then">;</span>
          </div>
          <div class="pFou">
            <span class="word">transitionName.value</span>
            <span class="then">=</span> <span class="then">"</span>
            <span class="src">listRight</span> <span class="then">"</span>
            <span class="then">;</span>
            <span class="comment">//按下一張到大於總長度->從右邊進來</span>
          </div>
          <div class="pTwo">
            <span class="brackets">}</span> <span class="then">else</span>
            <span class="brackets">{</span>
          </div>
          <div>
            <span class="comment">//決定播放哪種過場動畫</span>
          </div>
          <div>
            <span class="comment">
              //條件: 目前第幾張,是否小於總數 成立:從右邊進來 不成立:從左邊進來
            </span>
          </div>
          <div class="pFou">
            <span class="word">transitionName.value</span>
            <span class="then">=</span>
          </div>
          <div class="pSix">
            <span class="word">showCarousel.value </span>
            <span class="then">˂</span> <span class="word">index </span>
            <span class="then">? "</span><span class="src">listRight</span>
            <span class="then">" : "</span><span class="src">listLeft</span>
            <span class="then">";</span>
          </div>
          <div class="pFou">
            <span class="word">showCarousel.value </span>
            <span class="then">=</span> <span class="word">index</span>
            <span class="then">;</span>
          </div>
          <div class="pFou">
            <span class="comment"
              >//讓下方5個按鈕可以改變showCarousel的值來顯示指定的圖片</span
            >
          </div>
          <div class="pTwo">
            <span class="brackets">}</span>
          </div>
          <span class="brackets">}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.top5 {
  margin-top: 5px;
}
.top10 {
  margin-top: 10px;
}
section {
  width: 100vw;
  max-width: 100%;
}
.fz24 {
  font-size: 24px;
}
.mar5 {
  margin: 5px;
}
button {
  padding: 10px;
}

.carouselSection {
  height: 210px;
  width: 100vw;
  max-width: 100%;
  background-color: #daa520;
  display: flex;
  justify-content: center;
  align-items: center;
}

.carouselContainer {
  position: relative;
  width: 100vw;
  height: 210px;
  background-color: #000000;
  overflow: hidden;
}
.page {
  list-style: none;
  width: 100vw;
  height: 210px;
}
.pageImg {
  position: relative;
  width: 100%;
  z-index: 15;
}

.pageImg:hover {
  position: relative;
  transform: scale(1.3);
  transition: all 2s ease;
  z-index: 15;
}
.pageImgPOA {
  position: relative;
  width: 100%;
  z-index: 1;
  filter: blur(2px);
  transform: translate(0, -3%);
}

.carouselLeft {
  position: absolute;
  z-index: 50;
  top: 100px;
  left: 0;
}

.carouselRight {
  position: absolute;
  z-index: 50;
  top: 100px;
  right: 0;
}

/* right--------------------------------------------------------------------------------- */

.listLeft-enter-active,
.listLeft-leave-active {
  transition: all 2s ease;
}

.listLeft-enter-from {
  transform: translateX(-100%);
}
.listLeft-leave-to {
  transform: translateX(100%);
}

.listLeft-leave-active,
.listLeft-enter-active {
  position: absolute;
}

/* right--------------------------------------------------------------------------------- */

.listRight-enter-active,
.listRight-leave-active {
  transition: all 2s ease;
}

.listRight-enter-from {
  transform: translateX(100%);
}
.listRight-leave-to {
  transform: translateX(-100%);
}

.listRight-leave-active,
.listRight-enter-active {
  position: absolute;
}

.carouselOneToFive {
  width: 100vw;
  max-width: 100%;
  background-color: #c4c4c4;
  display: flex;
  justify-content: center;
}
</style>
