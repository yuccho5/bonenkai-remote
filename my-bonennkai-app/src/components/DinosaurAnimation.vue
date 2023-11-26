<template>
  <div class="animation-container">
    <!--<img class="background" src="@/assets/sky-background.png"> -->
    <img class="dinosaur" src="@/assets/dinosaur.png">
    <img class="lower-jaw" src="@/assets/dinosaur-lower-jaw.png">
    <img class="egg" v-show="isEggVisible" :style="eggStyle" src="@/assets/egg.png">
    <!--<img class="product" v-show="isProductVisible" src="@/assets/product.png"> -->
    <button class="start-button" v-if="!isAnimationStarted" @click="startAnimation">ガチャる</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEggVisible: false,
      eggStyle: { top: 'initial position' }, // 初期位置
      isProductVisible: false,
      isAnimationStarted: false,
    };
  },
  methods: {
    startAnimation() {
      this.isAnimationStarted = true;
      setTimeout(() => {
        this.isEggVisible = true;
        this.eggStyle.top = 'falling position'; // 卵が落ちるアニメーション
        setTimeout(() => {
          this.isProductVisible = true; // 商品画像の表示
        }, 2000); // 卵が落ちてから商品画像が表示されるまでの時間
      }, 2000); // 口が開いてから卵が表示されるまでの時間
    },
    resetAnimation() {
      // アニメーションをリセットするメソッド
    }
  }
};
</script>

<style scoped>
.animation-container {
  position: relative;
  width: 100%; /* コンテナの幅を指定 */
  height: 100vh; /* コンテナの高さを指定 */
  overflow: hidden; /* コンテナ外の要素を非表示にする */
}

.start-button {
  background-color: red; /* ボタンの背景色 */
  color: white; /* ボタンのテキスト色 */
  border: 2px solid gold; /* 金色の縁 */
  border-radius: 15px; /* 角丸の形状 */
  padding: 30px 60px; /* ボタン内の余白 */
  font-size: 40px; /* フォントサイズ */
  cursor: pointer; /* マウスオーバー時のカーソルをポインタに */
  transition: background-color 0.3s ease; /* 背景色の変化にトランジションを適用 */
  position: absolute; /* 絶対位置指定 */
  left: 15%; /* 画面の左側からの位置 */
  bottom: 30%; /* 画面の下側からの位置 */
}

.start-button:hover {
  background-color: darkred; /* ホバー時の背景色 */
}
.dinosaur {
  position: absolute;
  right: 15%; /* 位置を調整 */
  bottom: 15%; /* 位置を調整 */
  width: 60%; /* 画像のサイズを調整 */
}
.lower-jaw {
  position: absolute;
  right: 20%; /* 位置を調整 */
  bottom: 60%; /* 位置を調整 */
  width: 60%; /* 画像のサイズを調整 */
  transform: translateY(100%); /* 口を適切に位置させる */
}
.egg {
  position: absolute;
  right: 20%; /* 位置を調整 */
  bottom: 20%; /* 位置を調整 */
  width: 10%; /* 画像のサイズを調整 */
}
</style>
