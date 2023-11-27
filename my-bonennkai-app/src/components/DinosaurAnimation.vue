<template>
  <div class="animation-container">
    <!--<img class="background" src="@/assets/sky-background.png"> -->
    <img class="dinosaur" src="@/assets/dinosaur.png"> 
    <button class="start-button" v-if="!isAnimationStarted" @click="onStartClick">ガチャる</button>
  </div>
</template>

<script>
export default {
  /*data() {
    return {
      isEggVisible: false,
      eggStyle: { top: 'initial position' }, 
      isProductVisible: false,
      isAnimationStarted: false,
    };
  },*/

  methods: {
    onStartClick() {
      this.$emit('start'); // 親コンポーネントに通知
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
  /* animation: shake 0.5s ease infinite; /* アニメーションを適用 */
}

/* 揺れるアニメーションの定義 */
@keyframes shake {
  0%, 100% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-3px);
  }
  75% {
    transform: translateX(3px);
  }
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

</style>
